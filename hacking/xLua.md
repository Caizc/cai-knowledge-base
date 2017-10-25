# xLua

![](media/15035896643302.jpg)

# Documentation

[xLua 官方文档 - GitHub](https://github.com/Tencent/xLua/tree/master/Assets/XLua/Doc)
[xLua 教程](https://github.com/Tencent/xLua/blob/master/Assets/XLua/Doc/XLua%E6%95%99%E7%A8%8B.md)
[xLua API](https://github.com/Tencent/xLua/blob/master/Assets/XLua/Doc/XLua_API.md)

# 增加第三方 lua 库

## 阅读官方文档

[XLua 增加删除第三方 lua 库](https://github.com/Tencent/xLua/blob/master/Assets/XLua/Doc/XLua%E5%A2%9E%E5%8A%A0%E5%88%A0%E9%99%A4%E7%AC%AC%E4%B8%89%E6%96%B9lua%E5%BA%93.md)

## 下载开源项目源码

* [xLua-2.1.9](/var/folders/sm/__2_3yg10sbbbcn5k_d3p28r0000gn/T/.SKMClipboardFileOfPaste)
* [pbc-master](/var/folders/sm/__2_3yg10sbbbcn5k_d3p28r0000gn/T/.SKMClipboardFileOfPaste)
* lpeg
* lua-rapidjson
* [build_xlua_with_libs-master](/var/folders/sm/__2_3yg10sbbbcn5k_d3p28r0000gn/T/.SKMClipboardFileOfPaste)

## pbc 库编译配置

* 修改 **CMakeLists.txt**：

```
#begin lua-rapidjson
set (RAPIDJSON_SRC lua-rapidjson/source/rapidjson.cpp)
set_property(
	SOURCE ${RAPIDJSON_SRC}
	APPEND
	PROPERTY COMPILE_DEFINITIONS
	LUA_LIB
)
list(APPEND THIRDPART_INC  lua-rapidjson/include)
set (THIRDPART_SRC ${THIRDPART_SRC} ${RAPIDJSON_SRC})
#end lua-rapidjson

#begin lpeg
set ( LPEG_SRC
    lpeg/lpcap.c
    lpeg/lpcode.c
    lpeg/lpprint.c
    lpeg/lptree.c
    lpeg/lpvm.c
)
set_property(
    SOURCE ${LPEG_SRC}
    APPEND
    PROPERTY COMPILE_DEFINITIONS
    LUA_LIB
)
list(APPEND THIRDPART_INC  lpeg)
set (THIRDPART_SRC ${THIRDPART_SRC} ${LPEG_SRC})
#end lpeg

#begin pbc
set (PBC_SRC 
    pbc/src/alloc.c
    pbc/src/array.c
    pbc/src/bootstrap.c
    pbc/src/context.c
    pbc/src/decode.c
    pbc/src/map.c
    pbc/src/pattern.c
    pbc/src/proto.c
    pbc/src/register.c
    pbc/src/rmessage.c
    pbc/src/stringpool.c
    pbc/src/varint.c
    pbc/src/wmessage.c
	pbc/src/pbc-lua53.c
)
set_property(
    SOURCE ${PBC_SRC}
    APPEND
    PROPERTY COMPILE_DEFINITIONS
    LUA_LIB
)
list(APPEND THIRDPART_INC pbc pbc/src)
set (THIRDPART_SRC ${THIRDPART_SRC} ${PBC_SRC})
#end pbc
```

* 将 pbc 根目录下的 `pbc.h` 放置到 `pbc/src` 中
* 将 `pbc/binding/lua53` 目录下的 `pbc-lua53.c` 放置到 `pbc/src` 中

* 在 `pbc.h` 第 24 行增加：

```c
#ifdef _MSC_VER
typedef enum { false = 0, true = !false } bool;
#endif
```

在 `pbc-lua53.c` 的 `luaopen_protobuf_c` 方法前增加声明 `LUALIB_API`：

```c
LUALIB_API int luaopen_protobuf_c(lua_State *L) {
	luaL_Reg reg[] = {
		{"_env_new" , _env_new },
		{"_env_register" , _env_register },
		{"_env_type", _env_type },
		{"_rmessage_new" , _rmessage_new },
		{"_rmessage_delete" , _rmessage_delete },
		{"_rmessage_int", _rmessage_int },
		{"_rmessage_real" , _rmessage_real },
		{"_rmessage_string" , _rmessage_string },
		{"_rmessage_message" , _rmessage_message },
		{"_rmessage_size" , _rmessage_size },
		{"_wmessage_new", _wmessage_new },
		{"_wmessage_delete", _wmessage_delete },
		{"_wmessage_real", _wmessage_real },
		{"_wmessage_string", _wmessage_string },
		{"_wmessage_message", _wmessage_message },
		{"_wmessage_int", _wmessage_int },
		{"_wmessage_buffer", _wmessage_buffer },
		{"_wmessage_buffer_string", _wmessage_buffer_string },
		{"_pattern_new", _pattern_new },
		{"_pattern_delete", _pattern_delete },
		{"_pattern_size", _pattern_size },
		{"_pattern_unpack", _pattern_unpack },
		{"_pattern_pack", _pattern_pack },
		{"_last_error", _last_error },
		{"_decode", _decode },
		{"_gc", _gc },
		{"_add_pattern", _add_pattern },
		{"_add_rmessage", _add_rmessage },
		{"_env_enum_id", _env_enum_id},
		{NULL,NULL},
	};
```

* 在 Windows 系统中，生成 Windows 动态链接库

修改 `make_win32_lua53.bat` 和 `make_win64_lua53.bat` 中的 `cmake` 参数（可选），然后运行

```
// 如有必要，将
cmake -G "Visual Studio 14 2015 Win64" ..
// 修改为
cmake -G "Visual Studio 15 2017 Win64" ..
```

* 在 macOS 系统中，生成 OSX 动态链接库

```sh
$source make_osx_lua53.sh
```

* 在 macOS 系统中，生成 iOS 动态链接库

```sh
$source make_ios_lua53.sh
```

* 在 macOS 系统中，生成 Android 动态链接库

修改 `make_android_lua53.sh` 内容为：

```sh
if [ -z "$ANDROID_NDK" ]; then
    export ANDROID_NDK=/Users/zicongcai/Applications/Android/android-ndk-r14b/
fi

mkdir -p build_v7a && cd build_v7a
cmake -DANDROID_ABI=armeabi-v7a -DCMAKE_TOOLCHAIN_FILE=../cmake/android.toolchain.cmake -DANDROID_TOOLCHAIN_NAME=arm-linux-androideabi-4.9 -DANDROID_NATIVE_API_LEVEL=android-9 ../
cd ..
cmake --build build_v7a --config Release
mkdir -p plugin_lua53/Plugins/Android/libs/armeabi-v7a/
cp build_v7a/libxlua.so plugin_lua53/Plugins/Android/libs/armeabi-v7a/libxlua.so

mkdir -p build_x86 && cd build_x86
cmake -DANDROID_ABI=x86 -DCMAKE_TOOLCHAIN_FILE=../cmake/android.toolchain.cmake -DANDROID_TOOLCHAIN_NAME=x86-4.9 -DANDROID_NATIVE_API_LEVEL=android-9 ../
cd ..
cmake --build build_x86 --config Release
mkdir -p plugin_lua53/Plugins/Android/libs/x86/
cp build_x86/libxlua.so plugin_lua53/Plugins/Android/libs/x86/libxlua.so
```

```sh
$source make_android_lua53.sh
```

## 合并 Plugins 文件夹

将 `build/plugin_lua53/Plugins` 文件夹内容**并入**（注意，不是直接替换）`Assets/Plugins` 文件夹中。

## 编写 HelloWorld

* 将 build_xlua_with_libs-master 项目的 `LibsTestProj/Assets` 目录下的 **HelloWorld** 文件夹、**Resources** 文件夹和 **BuildInInit.cs** 文件拷贝到 xLua 项目的 `Assets` 目录下。
* 打开 Unity，运行 `HelloWorld.scene`，查看是否无报错且运行成功，如 log 内容符合预期则表示第三方 lua 库集成到 xLua 完毕。

---

change log: 

	- 创建（2017-08-14）
	- 更新（2017-08-24）

---

