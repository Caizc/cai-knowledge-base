# Google Protocol Buffers 的使用

[Protocol Buffers](https://developers.google.com/protocol-buffers/)
[Protocol Buffers 在游戏中的应用](http://disksing.com/pb-on-gamedev)
[从Protocol Buffers 到 gRPC](http://www.jianshu.com/p/6c9f90538efe)

## C# 整合 Protocol Buffers 3

[简单使用Protobuf-net（NuGet方式）](http://blog.csdn.net/u012741077/article/details/51213100)
[简单使用Protobuf-net（dll方式）](http://blog.csdn.net/u012741077/article/details/51290916)
[简单使用Protobuf-net（源码方式）](http://blog.csdn.net/u012741077/article/details/51292176)

[《Unity 3D游戏客户端基础框架》protobuf 导excel表格数据-客户端](http://blog.csdn.net/linshuhe1/article/details/52062969)
[《Unity 3D游戏客户端基础框架》protobuf网络框架-服务端](http://blog.csdn.net/linshuhe1/article/details/51781749)

## Java 整合 Protocol Buffers 3

[Protocol Buffer Basics: Java](https://developers.google.com/protocol-buffers/docs/javatutorial)

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

[Unity3D —— Socket通信(C#)](http://blog.csdn.net/linshuhe1/article/details/51386559)

---

change log: 

	- 创建（2017-08-22）
	- 更新（2017-08-28）

---

