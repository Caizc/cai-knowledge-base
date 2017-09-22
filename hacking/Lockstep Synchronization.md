# Lockstep Synchronization - 帧同步

## 特性

**确保所有 Client 的「确定性模拟」（将一盘游戏视为一个大状态机）**

* Client 基于**指令驱动**
* Client 统一**步进帧率**
* Client 每一步进帧向 Server **发送输入数据**，并加上**帧索引**
* 所有 Client 每一步进帧的**输入一致**
* 仅通过 Server **交换用户输入**
* Server 每一步进帧要收**集齐**所有 Client 输入再进入下一步进帧
* Server 在开始时为**所有 Client 同步初始帧索引**
* Server 为每一**步进帧分配索引编号**，并且打上**时间戳**
* 即使 Client 无操作也要向 Server 发送**锁步包**
* Server 发现步进帧中缺少某个 Client 的数据包，则广播时用**空数据包**代替
* Server 可以采用**「定时不等待」的乐观锁**进行步进帧消息广播
* Client 收到步进帧数据之后，**对帧无误后通知 Server 发送下一帧**，Client 可以缓存一定数量的帧
* Server 为所有 Client 分配**统一的「随机种子」**，实现 AI、技能的确定性模拟
* Client 使用**「定点数」取代「浮点数」**
* 逻辑层使用定点数，**显示层可以使用浮点数**（需做好定时校正）
* Client 使用**「确定性物理引擎」**取代 Unity 自带物理引擎
* Client **不可使用 Unity 的 Navmesh** 来自动寻路
* 由各个 **Client 自行计算模拟结果**，并渲染显示
* Client 按照**单机游戏实现**
* Client 的**逻辑层和显示层分离**
* 保存操作序列，**支持回放**
* 为**断线重连** Client 发送操作序列，**快进**赶上其他 Client 进度（显示层帧率可调）
* Client **快进期间不允许（不发送）操作**
* Client 缺失某一步进帧数据，会卡住自己，需要**向 Server 请求缺失的步进帧数据**
* Client **缓存一定数量的步进帧数据用于播放**，平滑网络抖动
* **减少需要帧同步的对象**，允许不影响逻辑的对象出现不一致（比如频繁发射的子弹）
* 优化时要考虑清楚**网络延迟和执行延迟**
* **使用 UDP，冗余帧数据来对抗丢包**，Client 请求缺失帧数据可以使用 TCP
* AI 行为设计保证可以「确定无误」地执行，即**「确定性的 AI」**
* 确保**所有 Client 的版本一致**，版本不一致无法进行游戏（匹配相同版本的玩家到同一个房间中）
* **Server 版本与 Client 版本的兼容问题**

* 以 Game Turn 游戏帧作为唯一的时间线，物品持续时间、状态持续时间都由此帧数控制
* Client 逻辑帧率可调
* Client 逻辑帧数与渲染帧数可作固定比例绑定

* **Lockstep Turn - 步进帧**，一个步进帧处理一次玩家操作，一个步进帧由多个游戏帧组成，一般是固定的
* **Game Turn - 游戏帧**，在游戏帧中处理游戏逻辑和物理模拟（这个待确认？），游戏帧的执行速率取决于性能，也可以处理成固定的
* **Action - 一次玩家操作指令**
* **Game Turn Frame -> 1 -> 2 -> 3 -> 4 -> Lockstep Turn Frame**，Lockstep Turn Frame 将 CTRL 数据给到 Client，Client 在 Game Turn Frame 的关键帧中收集当前 CTRL+1 数据发送到 Server，然后使用 CTRL 数据作为接下来 1、2、3、4 非关键帧中的虚拟操控数据

![](media/15052072029953.jpg)

**断线重连 & 快进支持：**

* Client 逻辑帧率可调，以加快模拟运算（或者可以跳过部分渲染帧？）
* Server 保存快照，给重连的 Client 发送快照

## Photon TrueSync

* 帧同步，仅交换输入，本地计算模拟（需要）
* 跨平台确定性物理引擎（需要）
* 自动回放（非必需）
* 回退和状态跟踪（非必需，优化提高项，使用起来有风险）
* 基于 Photon Unity Networking（PUN）构建，并完美兼容 PUN（非必需，除非使用了 Photon Server）

* PUN 提供了登录系统、房间系统，TrueSync 实现战斗同步
* PUN 还提供了 RPC 调用等特性

## 帧同步框架

**TrueSync 与 PUN 耦合的类：**

_PhotonTrueSyncCommunicator_
_TrueSyncManager_
_UnityUtils_

**TrueSync 使用到 PUN 的功能接口：**

_Photon.PunBehaviour_: This class provides a .photonView and all callbacks/events that PUN can call. Override the events/methods you want to use.

* OnJoinedLobby()：加入游戏大厅后的回调方法
Called on entering a lobby on the Master Server. The actual room-list updates will call OnReceivedRoomListUpdate().

_PhotonNetwork_

* PhotonNetwork.ConnectUsingSettings("v1.0")
* PhotonNetwork.automaticallySyncScene = true
* PhotonNetwork.JoinOrCreateRoom("room1", null, null)
* PhotonNetwork.playerList
* PhotonNetwork.isMasterClient
* PhotonNetwork.LoadLevel("_HelloWorld/Game")
* PhotonNetwork.connected
* PhotonNetwork.inRoom
* PhotonNetwork.networkingPeer
* PhotonNetwork.EventCallback
* PhotonNetwork.OnEventCall += lastEventCallback

_LoadBalancingPeer_

* loadBalancingPeer.RoundTripTime
* loadBalancingPeer.PeerState
* loadBalancingPeer.OpRaiseEvent(eventCode, message, reliable, eventOptions)

_ExitGames.Client.Photon.PeerStateValue_ ：enum

* ExitGames.Client.Photon.PeerStateValue.Connected

_RaiseEventOptions_

* RaiseEventOptions.TargetActors

_PhotonPlayer_ : 需要将 PhotonPlayer 转换为 TSPlayer

**问题：**

* 如何防止 TrueSync 发送空的数据包给 Server ？

---

change log: 

	- 创建（2017-09-13）
	- 更新（2017-09-16）

---

