# Google Protocol Buffers 的使用

* [Protocol Buffers Tutorial: C# - Google Develpers](https://developers.google.com/protocol-buffers/docs/csharptutorial)
* [Protocol Buffers](https://developers.google.com/protocol-buffers/)
* [Protocol Buffers 在游戏中的应用](http://disksing.com/pb-on-gamedev)
* [从Protocol Buffers 到 gRPC](http://www.jianshu.com/p/6c9f90538efe)

## Protocol Buffers 语法

* [Language Guide(proto2) - Google Developers](https://developers.google.com/protocol-buffers/docs/proto?hl=zh-cn)
* [Language Guide(proto3) - Google Developers](https://developers.google.com/protocol-buffers/docs/proto3?hl=zh-cn)
* [Protobuf2 语法指南 - 鸟窝](https://colobu.com/2015/01/07/Protobuf-language-guide/)
* [Protobuf3 语法指南 - 鸟窝](https://colobu.com/2017/03/16/Protobuf3-language-guide/)
* [Protocol Buffers 3 学习笔记 - gitbook](https://skyao.io/learning-proto3/)

## protobuf-net

* [protobuf-net - GitHub](https://protobuf-net.github.io/protobuf-net/version)
* [What version of ProtoBuf does protobuf-net use? - GitHub](https://protobuf-net.github.io/protobuf-net/version)

## C# 整合 Protocol Buffers 3

* [简单使用Protobuf-net（NuGet方式）](http://blog.csdn.net/u012741077/article/details/51213100)
* [简单使用Protobuf-net（dll方式）](http://blog.csdn.net/u012741077/article/details/51290916)
* [简单使用Protobuf-net（源码方式）](http://blog.csdn.net/u012741077/article/details/51292176)
* [Unity 跨 iOS、Android 平台使用 protobuf-net 的方法 - 程序园](http://www.voidcn.com/article/p-etdpvfcx-gt.html)
* [protobuf-net - GitHub](https://github.com/mgravell/protobuf-net)

* [《Unity 3D游戏客户端基础框架》protobuf 导excel表格数据-客户端](http://blog.csdn.net/linshuhe1/article/details/52062969)
* [《Unity 3D游戏客户端基础框架》protobuf网络框架-服务端](http://blog.csdn.net/linshuhe1/article/details/51781749)

## Java 整合 Protocol Buffers 3

* [Protocol Buffer Basics: Java](https://developers.google.com/protocol-buffers/docs/javatutorial)

* 定义协议格式
* 编译 Protocol Buffers 为 java 类

```
protoc -I=$SRC_DIR --java_out=$DST_DIR $SRC_DIR/addressbook.proto
```

## pbc 相关

* 在终端中，使用protoc编译命令生成pb文件

```shell
protoc -o message.pb message.proto
或者
protoc --descriptor_set_out test.pb message.proto
```

## 延伸阅读

* [Unity3D —— Socket通信(C#)](http://blog.csdn.net/linshuhe1/article/details/51386559)

## Protobuf 应用

* [我的 Protonbuf 消息设计原则 - OSCHINA](https://my.oschina.net/cxh3905/blog/159122?p=1)
* [我的 Protobuf 消息设计原则（续）- OSCHINA](https://my.oschina.net/cxh3905/blog/293000?p=1)
* [一种自动反射消息类型的 Google Protobuf 网络传输方案 - 陈硕的 Blog](https://www.cnblogs.com/Solstice/archive/2011/04/03/2004458.html)

## proto3 与 proto2 的区别

* [Protocol Buffer 的 proto3 与 proto2 的区别 - CSDN](https://blog.csdn.net/huanggang982/article/details/77944174)
* [proto3 默认值与可选项 - Tech For Fun](http://kaelzhang81.github.io/2017/05/15/proto3%E9%BB%98%E8%AE%A4%E5%80%BC%E4%B8%8E%E5%8F%AF%E9%80%89%E9%A1%B9/)

---

change log: 

	- 创建（2017-08-22）
	- 更新（2017-08-28）
	- 更新（2019-05-22）

---

