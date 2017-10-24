# Network Frameworks work with Unity - 网络框架

## IceWorld

* 出自《Unity 5.X 3D游戏开发技术详解与典型案例》中的 Demo
* 基于异步 Socket 实现
* Java 服务端
* 完成度低，仅是一个初级的 Demo
* 代码结构混乱，注释少
* 已整理调试通过

## cocosocket

* GitHub 开源项目
* Java 服务端，使用了 Netty 组件
* C# 客户端，集成了 protobuf-net 库，支持 Google Protocol Buffers 协议
* 使用「逻辑帧」处理了分包粘包问题，具备事件监听回调、自定义协议解析器、消息队列等功能特性
* 较为完善的类结构，具备基本的框架结构，方便后续扩展
* 据说是应用于实际项目中的网络框架
* 代码注释尚可
* 已通过初步调试，具体实现原理需进一步深入研究

## Tank Client & Server

* 出自《Unity 3D 网络游戏实战》的完整案例
* 基于异步 Socket 实现
* C# 服务端和客户端
* 服务端使用了 MySQL 数据库
* 自定义协议格式的简单实现
* 代码结构清晰，注释清晰，配套书籍详细讲解
* 如果应用起来最好将 C# 服务端修改为 Java 实现
* 功能特性较为齐全，但实用性未知

## Photon Unity Networking

[Photon Unity Networking Free - Unity Asset Store](https://www.assetstore.unity3d.com/cn/#!/content/1786)
[PUN Documentation](https://doc.photonengine.com/en-us/pun/current/getting-started/pun-intro)
[PUN API](https://github.com/Caizc/learn-photon-truesync)

* 收费的成熟商业网络引擎
* 功能全面，有官方英文文档和 API 手册，但没有开发者社区，国内使用者少，中文资料少

## KBEngine

[KBEngine](http://kbengine.org/cn/)
[kbengine - GitHub](https://github.com/kbengine/kbengine)

> 一款开源的游戏服务端引擎，客户端通过简单的约定协议就能与服务端通讯，使用 KBEngine 插件能够快速与(Unity3D、UE4、OGRE、HTML5、等等)技术结合形成一个完整的客户端。 服务端底层框架使用 C++ 编写，游戏逻辑层使用 Python(支持热更新)，开发者无需重复的实现一些游戏服务端通用的底层技术，将精力真正集中到游戏开发层面上来，快速的打造各种网络游戏。

## UNet

[如何评价Unity5中多人游戏和网络模块UNet？](https://www.zhihu.com/question/38842804)

## Reference

[Protobuf 与 Java（还提到了 Netty 的使用）](http://shift-alt-ctrl.iteye.com/blog/2210885)

---

change log: 

	- 创建（2017-08-31）
	- 更新（2017-09-21）

---

