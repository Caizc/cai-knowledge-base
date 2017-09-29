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
* Client 收到步进帧数据之后，**对帧无误后通知 Server 发送下一帧**，Client 缓存一定数量的帧用于播放
* Server 根据所有 Client 的**网络延迟动态调整帧率**
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

**特性对比：**

| 特性 | 必要特性 | 简化实现 | TrueSync |
| --- | --- | --- | --- |
| 指令驱动 | ✅ | ✅ | ✅ |
| 统一步进帧率 | ✅ | ✅ | ✅ |
| Server 帧序号 | ✅ | ✅ |  |
| Server 帧时间戳 | ✅ | ✅ |  |
| Client 锁步包 |  |  |  |
| 缺失 Client 输入广播空包 | ✅ | ✅ |  |
| 「定时不等待」乐观锁 | ✅ | ✅ |  |
| Client 对帧后通知 Server 继续下一帧 |  |  |  |
| Client 帧缓存 | ✅ | ✅ | ✅ |
| 统一随机种子 | ✅ |  | ✅ |
| 定点数取代浮点数 | ✅ |  | ✅ |
| 确定性物理引擎 |  |  | ✅ |
| 逻辑层与显示层分离 | ✅ | ✅ |  |
| 回放支持 |  |  |  |
| 断线重连 |  |  |  |
| Client 帧率动态调整 | ✅ | ✅ |  |
| Server 帧率动态调整 |  |  |  |
| 向 Server 请求缺失帧数据 | ✅ |  |  |
| UDP 协议支持 | ✅ |  |  |
| 确定性 AI |  |  |  |
| 版本兼容 | ✅ |  |  |

## Photon TrueSync

* 帧同步，仅交换输入，本地计算模拟（需要）
* 跨平台确定性物理引擎（需要）
* 自动回放（非必需）
* 回退和状态跟踪（非必需，优化提高项，使用有风险）
* 基于 Photon Unity Networking（PUN）构建，并完美兼容 PUN（非必需，除非使用了 Photon Server）

* PUN 提供了登录系统、房间系统，TrueSync 实现战斗同步
* PUN 还提供了 RPC 调用等特性

## TrueSync 从 PUN 基础上剥离

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

## TrueSync 解构

### 核心类

_TrueSyncManager_
管理 Player Prefab 的创建和 Lockstep 流程的执行，提供引擎主要功能特性的 API 接口

1. **Awake()**

    - 加载配置
    - 初始化 Rollback 窗口大小
    - 初始化 TSRandom 随机类
    - 初始化物理引擎 PhysicsManager
    - 初始化状态跟踪器
    
2. **Start()**

    - 初始化 PUN 网络通信接口
    - 初始化 Lockstep 引擎，向 AbstractLockstep 传入配置参数和帧同步生命周期回调方法
    - 加载回放记录
    - 附加 TrueSync 状态显示组件
    - 初始化协程调度器 CoroutineScheduler
    - 将 PhotonPlayer 转换为 TSPlayer，初始化玩家队列
    - 初始化场景中动态生成的 Player 对象实体，将其中继承了 TrueSyncBehaviour 的组件注册到 TrueSyncManagedBehaviour 中集中管理，并初始化这些托管组件中的 Player 信息
    - 初始化场景中通用的 TrueSyncBehaviour 组件，处理过程与上一个步骤相似
    - 为物理引擎 PhysicsManager 注册 OnRemovedRigidBody 回调
    - 标记「开始状态」为 `BEHAVIOR_INITIALIZED`

3. **FixedUpdate()**

    - 更新所有协程 CoroutineScheduler.UpdateAllCoroutines()
    - 执行一次帧逻辑 Lockstep.Update()

4. **Update()**

    - 更新 startState
    - 调用 Lockstep engine 执行模拟 RunSimulation

5. **GetLocalData(InputDataBase)**

    - 设置 TrueSyncInput 中的当前输入数据容器 currentInputData 为刚刚从资源池中取出来的「新的」 SyncedData 对象中的 InputData
    - 调用每个 Player 所有的 TrueSyncBehaviour 组件的 OnSyncedInput()，收集这一帧的输入信息保存到 InputData 对象中

6. **OnStepUpdate(List<InputDataBase>)**

    - CheckGameObjectsSafeMap，安全检查，移除标记为 Destroy 的 GameObject
    - TrueSyncInput.SetAllInputs(null)，清空所有输入数据
    - 调用场景中所有通用 TrueSyncBehaviour 组件的 OnPreSyncedUpdate 方法，更新所有协程
    - 调用所有 Player 相关 TrueSyncBehaviour 组件的 OnPreSyncedUpdate 方法，更新所有协程
    - TrueSyncInput.SetAllInputs(allInputData)，设置所有输入数据
    - 调用场景中所有通用 TrueSyncBehaviour 组件的 OnSyncedUpdate 方法，更新所有协程
    - 调用所有 Player 相关 TrueSyncBehaviour 组件的 OnSyncedUpdate 方法，更新所有协程
    - CheckQueuedBehaviour ?

7. **CheckGameObjectsSafeMap()**

    - 移除场景中标记为 Destroy 的 GameObject ？

8. **CheckQueuedBehaviour()**

    - 检查 queuedBehaviours 列表中 TrueSyncManageBehaviour 组件
    - 调用 TrueSyncManageBehaviour 中组件的 OnSyncedStart 方法
    - 清空 queuedBehaviours 列表

_AbstractLockstep_
Lockstep engine 的抽象处理逻辑

1. **NewInstance()**

    - 根据配置中回滚窗口大小和是否有网络通信接口决定实例化 DefaultLockstep 还是 RollbackLockstep 帧锁定引擎实现类

2. **AbstractLockstep()**

    - 构造方法，初始化所有成员变量

3. **Update()**

    - 如果正在等待玩家，则向玩家发送「开始同步」消息
    - 否则更新界面的同步状态显示
    - 检查是否有玩家掉线
    - 检查帧数据是否已准备好
    - 如果数据已准备好，则发送 Player InputData 帧数据到 Server，重置 ElapsedPanicTicks 丢帧危险计数
    - 然后每隔 100 帧向 Server 发送信息校验和 SendInfoChecksum
    - 更新最后的安全帧 lastSafeTick 为当前帧
    - BeforeStepUpdate，在步进到下一帧的模拟状态之前，检查安全性，移除需要 Destroy 的对象和掉线的 Player
    - 获取同步窗口 SyncWindow（配置中指定）帧数之前的帧数据（向 Server 发送的 InputData 和执行当前帧所用的 InputData 相差 SyncWindow 个帧，用来补偿网络延迟）
    - 执行帧逻辑 ExecutePhysicsStep（重要）
    - AfterStepUpdate，移除 ActivePlayers 已执行过的帧数据
    - 增加 tick 计数
    - 否则增加错过的帧计数，增加 ElapsedPanicTicks 丢帧危险计数（超过阈值则结束帧同步，踢掉延迟过大的玩家）
    - 执行物理引擎的 Update()
    - 更新数据 UpdateData()
    - 增加 tick 计数

4. **RunSimulation()**

    - 调用 Run() 执行模拟
    - 如果不是首次执行模拟，则向 Server 发送一个模拟帧

5. **Run()**

    - 根据 SimulationState 状态，确定目前 Lockstep engine 是处于等待玩家状态、暂停状态或者是运行状态，并调用相应的 OnGameStarted()、OnGameUnPaused() 回调方法

6. **UpdateData()**

    - 从资源池中取出一个新的同步数据容器 SyncedData，将本地 Player 的输入数据放入其中，再将该同步数据容器添加到 LocalPlayer 的 control 数据中
    - 获取 LocalPlayer 当前帧 tick 的待同步数据 SyncedData 数组（可以设置每一逻辑帧发送多少个 tick 的 SyncedData，这里默认为 1）
    - 将待同步数据 SyncedData 数组编码为 byte[] 后，调用底层网络通信接口 PhotonTrueSyncCommunicator，发送该模拟帧到 Server

7. **SendInfoChecksum(int)**

    - MD5 校验？

8. **CheckSafeRemotion(int)**

    - 检查安全移动？

9. **ExecutePhysicsStep(List<SyncedData>,int)**

    - ExecuteDelegates，执行一些常规的委托，检查 Player 是否掉线？
    - SyncedArrayToInputArray，将数据从 SyncedData 取出转移到 InputData 中
    - StepUpdate，使用刚取出的 InputData 作为输入执行该帧逻辑
    - PhysicsManager.UpdateStep()，物理模拟步进？

10. **AfterStepUpdate(int, int)**

    - 移除 ActivePlayers 已执行过的帧数据

11. **OnEventDataReceived(byte, object)**

    - 接收到底层网络回传的帧数据包
    - 将 byte[] 解码为 SyncedData List
    - 找到帧数据包对应的 TSPlayer，检查它是否掉线
    - 将 SyncedData 数据添加给对应的 TSPlayer
    - 将 SyncedData List 放回资源池

12. **OnSyncedDataReceived(TSPlayer, List<SyncedData>)**

    - TSPlayer.AddData(List<SyncedData>)

_TrueSyncBehaviour_
连接到游戏中的在不同设备上模拟运行的每个 Player 的行为抽象

_TrueSyncManagedBehaviour_
托管的 TrueSyncBehaviour 类，TrueSyncBehaviour 实现类的封装，负责调用 TrueSyncBehaviour 的自定义扩展脚本中的父类方法

_PhotonTrueSyncCommunicator_
TrueSync 对 ICommunicator 接口的实现，负责与底层网络引擎通信

1. RoundTripTime()

2. OpRaiseEvent(byte, object, bool, int[])

3. AddEventListener(OnEventReceived)

_TSPlayer_
帧同步玩家抽象

1. **AddData(SyncedData)**

    - 添加新的待同步的帧数据
    - 以帧序号 tick 判断是否已有该帧数据
    - 如果还没有该帧的数据则为该 Player 添加该 SyncedData，记录 lastTick = tick，否则丢弃该 SyncedData

2. **GetData(int)**

    - 根据帧序号 tick 获取玩家同步数据 SyncData
    - 如果没有当前帧序号的同步数据，则获取 tick - 1 即上一帧的同步数据
    - 如果连上一帧的同步数据都没有，就从资源池取一个「新的」 SyncedData 并初始化它为「假」（fake）数据

3. **RemoveData(int)**

    - 移除该 Player 某一帧的 SyncedData 容器，将该对象放回资源池中

_TSPlayerInfo_
帧同步玩家信息

_TrueSyncInput_
管理 Player 的输入信息

_InputData_
提供 Player 的输入信息

1. **Serialize(List<byte>)**

    - 将该 InputData 中的所有字典成员变量都序列化到 byte List 中（追加）

2. **Deserialize(byte[], ref int)**

    - 将 byte[] 中的数据反序列化为该 InputData 相应字典成员变量中的键值对（追加）

_SyncedData_
同步的数据，ResourcePoolItem 资源池物品的扩展

1. **Init()**

    - 初始化输入信息 InputData 的所有者、tick、fake、dirty 这些成员变量

2. **Encode(SyncedData[])**

    - 为 SyncedData 添加头部信息
    - 序列化 SyncedData 数组
    - 返回编码后的 byte[]

3. **GetEncodedHeader(List<byte>)**

    - 获取数据编码后的头部，包括该同步数据的所有者、掉线玩家 ID、是否掉线玩家标识

4. **GetEncodedActions(List<byte>)**

    - 获取 InputData 序列化后的 byte List

5. **Decode(byte[])**

    - 将 byte 数组解码为 SyncedData List

_SyncedInfo_
同步的信息

_ResourcePool_
资源池抽象

_ResourcePoolItem_
资源池物品接口

_ResourcePoolSyncedData_
继承于 ResourcePool<SyncedData> 的资源池同步数据类

1. **NewInstance()**

    - 获取新的 SyncedData 对象

2. **FillStack(int)**

    - 向资源池中初始化制定数量的新 SyncedData 对象

_GenericBufferWindow_
通用缓存窗口

_StateTracker_
状态跟踪类（与 Rollback 相关）

_SerializableDictionary_
序列化字典

_ReplayRecord_
回放记录

_CoroutineScheduler_
协程调度器

1. **UpdateAllCoroutines()**

-------

_DefaultLockstep_
Lockstep engine 的默认实现

_RollbackLockstep_
Lockstep engine 的回滚实现

_ICommunicator_
Lockstep engine 与底层网络引擎的通信接口

_ITrueSyncBehaviour_
TrueSync 抽象行为接口（Game 层面）

_ITrueSyncBehaviourCallbacks_
TrueSync 抽象行为回调接口（帧同步层面）

_ITrueSyncBehaviourGameplay_
TrueSync 抽象行为接口（GamePlay 中）

-------

_Stats_
状态类

_ChecksumExtractor_
校验和提取器

_TrueSyncStats_
状态信息显示

_TrueSyncConfig_
TrueSync 的配置集合

_TrueSyncExtensions_
Unity 基础组件类与 TrueSync 自定义基础组件类的转换工具集

_UnityUtils_
提供了一些工具函数

### 核心组件

_Math_
数学库

_Physics_
物理库

_Coroutine_
协程库

_Unity_
TrueSync 的对外的主要接口类

---

change log: 

	- 创建（2017-09-13）
	- 更新（2017-09-29）

---

