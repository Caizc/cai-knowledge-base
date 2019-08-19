# SuperSocket 的使用

## References

* [SuperSocket](http://www.supersocket.net/)
* [SuperSocket - GitHub](https://github.com/kerryjiang/SuperSocket)
* [SuperSocket.ClientEngine - GitHub](https://github.com/kerryjiang/SuperSocket.ClientEngine)
* [SuperSocket.ProtoBase - GitHub](https://github.com/kerryjiang/SuperSocket.ProtoBase)

## SuperSocket 集成 Protocol Buffer

### 参考

* [SuperSocket 与 Netty 之实现 protobuf 协议，包括服务端和客户端 - cnblogs](http://www.cnblogs.com/caipeiyu/p/5559112.html)
* [SuperSocket 集成 protobuf 的一个 Demo 项目 - GitHub](https://github.com/kotcmm/SuperSocket.ClientEngine.QuickStart)
* [SuperSocket 与 SuperSocket.ClientEngine 实现 Protobuf 协议 - cnblogs](https://www.cnblogs.com/linxmouse/p/7905575.html)

### SuperSocket ProtobufServer 搭建

1. 新建一个 ProtobufServer 项目
2. 从 NuGet 获取 **protobuf**、**SuperSocket** 和 **SuperSocket.Engine** 的依赖包

* 添加 protobuf 依赖包的搜索词是 `Google.ProtocolBuffers`
* 添加 SuperSocket 依赖包的搜索词是 `SuperSocket`

3. protobuf 协议定义和 C# 文件生成

* 定义 `BackMessage.proto`

```proto
message BackMessage{
    optional string content = 1;
}
```

* 定义 `CallMessage.proto`

```proto
message CallMessage{
    optional string content = 1;
}
```

* 定义 `DefeatMessage.proto`

```proto
import "BackMessage.proto";
import "CallMessage.proto";

message DefeatMessage{
    enum Type {CallMessage = 1; BackMessage = 2;}
    required Type type = 1;
    optional CallMessage callMessage = 2;
	optional BackMessage backMessage = 3;
}
```

* 使用项目目录 `packages\Google.ProtocolBuffers.2.4.1.555\tools` 中的 `protoc.exe` 和 `protogen.exe`，依次执行以下 cmd 命令（注意修改命令中的路径），生成 C# 代码

```cmd
protoc --descriptor_set_out=DefeatMessage.protobin --proto_path=./ --include_imports DefeatMessage.proto

protogen DefeatMessage.protobin
```

* 将生成的 `BackMessage.cs`、`CallMessage.cs` 和 `DefeatMessage.cs` 添加到项目中

4. 实现 `IRequestInfo` 接口，实现 `ProtobufRequestInfo.cs`
5. 实现 `IReceiveFilter<ProtobufRequestInfo>, IOffsetAdapter, IReceiveFilterInitializer` 接口，实现 `ProtobufReceiveFilter.cs`
6. 实现 `ProtobufAppSession.cs`
7. 实现 `ProtobufAppServer.cs`
8. 实现 Server 启动入口类

### SuperSocket ProtobufClient 搭建

1. 新建一个 ProtobufClient 项目
2. 从 NuGet 获取 **protobuf**、**SuperSocket.ClientEngine** 和 **SuperSocket.ProtoBase** 的依赖包

* 添加 protobuf 依赖包的搜索词是 `Google.ProtocolBuffers`
* 添加 SuperSocket 依赖包的搜索词是 `SuperSocket`

3. 将与服务端相同的 `BackMessage.cs`、`CallMessage.cs` 和 `DefeatMessage.cs` 添加到项目中
4. 实现 `IPackageInfo` 接口，实现 `ProtobufPackageInfo.cs`
5. 实现 `ProtobufReceiveFilter.cs`
6. 实现 Client 启动入口类
7. 分别启动 ProtobufServer 和 ProtobufClient，测试前后端通信是否成功

---

change log: 

	- 创建（2019-08-18）

---

