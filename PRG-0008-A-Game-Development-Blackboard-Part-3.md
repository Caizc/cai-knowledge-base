# Game Development Blackboard - Part 3

## 2025-06-28 星期六

### UE Lyra Starter Game

* [Lyra Starter Game - Epic Developer Community](https://dev.epicgames.com/community/learning/paths/Z4/lyra-starter-game)
* [UE5 Exploring Lyra - YouTube](https://youtu.be/xy2J-KnuzQs?si=ui7N3lS7DkOU5jTt)
* [UE5 Lyra 项目拆解 - 知乎](https://www.zhihu.com/column/c_1597245821048541184)
* [UE5 Lyra 示例项目解读 - 知乎](https://zhuanlan.zhihu.com/p/518029029)
* [UE5 Lyra 项目的解析与学习 - 知乎](https://zhuanlan.zhihu.com/p/690425805)
* [UE5 Lyra 的数据驱动之数据加载与引用 - 知乎](https://zhuanlan.zhihu.com/p/505766201)
* [UE5 Lyra 自定义 GameFeature AddWidget 类/ UI 框架 - 知乎](https://zhuanlan.zhihu.com/p/506574041)
* [UE5 新项目 Gameplay 框架设计（以 Lyra 为例）- 知乎](https://zhuanlan.zhihu.com/p/614718286)

### UI 框架

* [UE4 基于栈状态机的 UI 管理（框架设计）](https://www.yuewu.dev/posts/ue4-stack-state-based-ui-management)
* [UE5 CommonUI 框架 - 知乎](https://zhuanlan.zhihu.com/p/698935180)

### Messaging

* [GenericMessagePlugin - GitHub](https://github.com/wangjieest/GenericMessagePlugin)
* [UE Generic Message Plugin 插件原理篇 - 知乎](https://zhuanlan.zhihu.com/p/377632346)

## 2025-05-18 星期日

### UE Learning

* [BeginPlay - UE Learning](https://dev.epicgames.com/community/learning/paths/0w/unreal-engine-beginplay)

### UE5 MetaHuman and Cloth

* [The Only MetaHuman Tutorial You Need - YouTube](https://youtu.be/9L3rgTvMN0c?si=K43AywurSVNmE4Ip)
* [The Only Cloth Simulation Tutorial You Need - YouTube](https://www.youtube.com/watch?v=Z57ggNKZDy8)

## 2025-04-14 星期一

### Windows 路径长度限制

* [Maximum Path Length Limitation - Microsoft](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry)
* [How to change the default 256 character path limitation in Windows 10](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/The-Windows-10-default-path-length-limitation-MAX-PATH-is-256-characters.html)

### Building Unreal Engine from source

* [Setting Up Visual Studio - UE Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine)
* [Building Unreal Engine from source - UE Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source)

### Unreal Engine Installed Build

* [Versioning of Binaries](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-version-binaries-in-unreal-engine?application_version=5.5)

如果不希望每次构建 Installed Build 生成的所有二进制文件都发生改变，可以在 `/Engine/Build/Build.version` 文件中，加入 `BuildId` 字段来填写自定义的构建 ID。

* [Installed Build Reference Guide - UE Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine)

```shell
cd Engine\Build\BatchFiles
.\RunUAT.bat BuildGraph -target="Make Installed Build Win64" -script="Engine/Build/InstalledEngineBuild.xml" -clean -set:HostPlatformOnly=true -set:WithDDC=false

cd Engine\Build\BatchFiles
.\RunUAT.bat BuildGraph -target="Make Installed Build Win64" -script="Engine/Build/InstalledEngineBuild.xml" -clean -set:HostPlatformOnly=true -set:WithDDC=false -set:GameConfigurations=Development
```

### Using Perforce

* [What Is Perforce Streams? - YouTube](https://youtu.be/HaRsCVLNoxA?si=plKw1rMbnFZs0lI1)
* [Perforce Streams Quickstart - YouTube](https://youtu.be/ggty1lkL1gA?si=fUFKjD2sMlNS279M)

### Using UnrealGameSync(UGS)

* [UnrealGameSync(UGS) - UE Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine)
* [Unreal Game Sync - YouTube](https://youtu.be/xuEXqZ0nE70?si=A-BX7f4jrAPXyaY-)
* [Working with Custom Unreal Engine Builds & Unreal Game Sync - YouTube](https://youtu.be/ItLANIVz8UA?si=_88-tgHYP6X-Zfwe)
* [WiX v3](https://docs.firegiant.com/wix/wix3/)
* [UGS Troubleshooting - UE Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-troubleshooting)

## 2023-05-10 星期三

### Timezone 时区

* [彻底弄懂 GMT、UTC、时区和夏令时 - 知乎](https://zhuanlan.zhihu.com/p/135951778)
* [各大洲时区以及 Linux 环境下修改时区 - CSDN](https://blog.csdn.net/qq330983778/article/details/103465258)

### RSA

* [RSA 加密、解密、签名、验签的原理及方法](https://www.cnblogs.com/pcheng/p/9629621.html)

> 总结：公钥加密、私钥解密、私钥签名、公钥验签

## 2023-01-19 星期四

### Oodle Compression

* [Reducing Package Sizes with Oodle Compression - Epic Games Dev Community](https://dev.epicgames.com/community/learning/tutorials/ry2D/unreal-engine-reducing-package-sizes-with-oodle-compression)
* [Oodle Data Compression](http://www.radgametools.com/oodlecompressors.htm)

![oodle260_typical_combined](media/PRG-0008-A-Game-Development-Blackboard-Part-3/oodle260_typical_combined-1674142653839-2.png)

![image-20230119222430794](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20230119222430794.png)

## 2022-11-26 星期六

### Windows 线程栈空间

* [线程堆栈大小 - MSDN](https://learn.microsoft.com/zh-cn/windows/win32/procthread/thread-stack-size?redirectedfrom=MSDN)
* [Set Stack Size - Learn Microsoft](https://learn.microsoft.com/en-us/cpp/build/reference/f-set-stack-size?view=msvc-170)
* [OverrideStackSize - UE4 Documentation](https://docs.unrealengine.com/4.26/en-US/API/Runtime/Core/Misc/FQueuedThreadPool/OverrideStackSize/)

## 2022-11-16 星期四

### iOS App Rating

* [设计 iOS 评分引导 - 知乎](https://zhuanlan.zhihu.com/p/567156652)
* [Ratings and reviews - Apple Developer](https://developer.apple.com/design/human-interface-guidelines/patterns/ratings-and-reviews/)
* [SKStoreReviewController - Apple Developer](https://developer.apple.com/documentation/storekit/skstorereviewcontroller)
* [Requesting App Ratings and Reviews Tutorial for iOS - Kodeco](https://www.kodeco.com/9009-requesting-app-ratings-and-reviews-tutorial-for-ios)
* [Increase App Ratings by using SKStoreReviewController - SwiftLee](https://www.avanderlee.com/swift/skstorereviewcontroller-app-ratings/)

> ## SKStoreReviewController Limitations
>
> Apple does enforce certain limitations on how you use this API:
>
> - No matter how many times you request the review prompt, the system will show the prompt a maximum of three times in a 365-day period.
> - Calling the method is not a guarantee that the prompt will display. This means that it’s not appropriate to call the API in response to a button tap or other user action.
> - The system must not have shown the prompt for a version of the app bundle that matches the current bundle version. This ensures that the user is not asked to review the same version of your app multiple times.
>
> *Note*: The review prompt will behave differently depending on the type of build that you are running:
>
> - *Development*: Shown every time the you request the prompt.
> - *Test Flight*: Prompt is never shown.
> - *App Store*: Shown with the limitations described above.

## 2022-11-09 星期三

### UE4 自定义编译选项

* [How to use custom compiler options? - Epic Games Dev Community](https://forums.unrealengine.com/t/how-to-use-custom-compiler-options/409262)

> ﻿In VCToolChain.cs (\Engine\Source\Programs\UnrealBuildTool\Windows\VCToolChain.cs) you can append additional compilation argument in AppendCLArguments_Global() or AppendCLArguments_CPP(), if it’s c++ specific arguments.
>
> You can do that for every platform you need, (Linus, Mac, IOS, Android, etc) in their respective ToolChain file (LinuxToolChain.cs, for example).

## 2022-10-23 星期日

### UE4 多线程

* [UE4_MultiThread - GitHub](https://github.com/tiax615/UE4_MultiThread)

  ![image-20221023224323237](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20221023224323237.png)

* [《Exploring in UE4》多线程机制详解[原理分析] -知乎](https://zhuanlan.zhihu.com/p/38881269)

## 2022-10-08 星期六

### UE4 File Management

* [File and Folder Management, Create, Find, Delete - Unreal Engine Community Wiki](https://unrealcommunity.wiki/file-and-folder-management-create-find-delete-et2g64gx)

## 2022-09-10 星期六

### Texture Streaming in UE4

* [Managing the Texture Streaming Pool - YouTube](https://youtu.be/uk3W8Zhahdg)
* [Texture Streaming Configuration - UE Documentation](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/Textures/Streaming/Config/)

## 2022-09-04 星期日

### iOS mouse support in UE4

* [Bring keyboard and mouse gaming to iPad - Apple Developer](https://developer.apple.com/videos/play/wwdc2020/10617/)

![image-20220904022807097](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220904022807097.png)

```c++
// Engine/Source/Runtime/ApplicationCore/Private/IOS/IOSView.cpp

- (BOOL)prefersPointerLocked
{
    UE_LOG(LogIOS, Log, TEXT("IOSViewController prefersPointerLocked"));
    return YES; // Change the return value to NO to unlock the pointer
}
```

### iOS Home Indicator

* [How to force user to swipe twice home indicator to go home-screen? - stackoverflow](https://stackoverflow.com/questions/47347403/iphone-x-how-to-force-user-to-swipe-twice-home-indicator-to-go-home-screen)

```c++
// Engine/Source/Runtime/ApplicationCore/Private/IOS/IOSView.cpp

/**
 * Tell the OS to hide the home bar
 */
- (BOOL)prefersHomeIndicatorAutoHidden
{
	// return YES; // If return YES, the user swipe only once to go to the home screen, but the home indicator will auto hide completely.
	return NO; // If return NO, force the user swipe twice to go to the home screen, but the gray home indicator will stay on the bottom on the screen.
}
```

## 2022-07-27 星期三

### Rider 显示导航栏

* [File directory path/breadcrumbs missing in Rider for Windows?](https://www.reddit.com/r/Jetbrains/comments/suwgqg/file_directory_pathbreadcrumbs_missing_in_rider/)

![6QMbSCp](media/PRG-0008-A-Game-Development-Blackboard-Part-3/6QMbSCp-16588726411512.png)

### Rider 代码自动换行的字数设置

![image-20220821202540017](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220821202540017.png)

### UE4 Pak 加密与解密

* [Singing and Encryption - UE Documentation](https://docs.unrealengine.com/4.26/en-US/Basics/Projects/Packaging/#signingandencryption)
* [UE4 Pak 加密与解密调研 - 知乎](https://zhuanlan.zhihu.com/p/523750676)

### MD5 检查

```shell
#Mac
md5 [filename]

#Windows
certutil -hashfile [filename] md5
```

## 2022-07-04 星期一

### iOS 语言本地化

* [Localize 'plist' and 'NSLocalizedString' in an iOS Project - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/iOS/LocalizePlistInIOSProject/)
* [App Store 介绍页中显示的语言列表如何设置 - 简书](https://www.jianshu.com/p/92c21eb71537)
* [3 分钟实现 iOS 语言本地化/国际化 - 腾讯云开发者社区](https://cloud.tencent.com/developer/article/1143302)

### iOS 产品页优化

* [产品页优化 - Apple Developer](https://developer.apple.com/cn/app-store/product-page-optimization/)
* [Xcode 配置多套 App 图标的方法 - 稀土掘金](https://juejin.cn/post/7044748618078617613)
* [iOS 动态更换 APP 图标 - 简书](https://www.jianshu.com/p/e34b9805b424)
* [Dynaminally Change the App Icon - medium](https://medium.com/ios-os-x-development/dynamically-change-the-app-icon-7d4bece820d2)

## 2022-06-08 星期三

### iOS TestFlight

* [iOS 之 TestFlight 的使用教程 - 简书](https://www.jianshu.com/p/478a8c35cbe0)

### 移动端息屏

* [移动端息屏控制 - 虚幻社区知识库](https://ue5wiki.com/wiki/14280/)

## 2022-05-27 星期五

### Android APK 签名

* [Android v1 v2 v3 签名详解 - 知乎](https://zhuanlan.zhihu.com/p/89126018)
* [对应用进行签名 - Android Developers](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)
* [应用签名 - Android Source](https://source.android.com/security/apksigning)
* [APK 签名方案 v2 - Android Source](https://source.android.com/security/apksigning/v2)
* [APK 签名方案 v3 - Android Source](https://source.android.com/security/apksigning/v3)
* [apksigner - Android Developers](https://developer.android.com/studio/command-line/apksigner)
* [Android APK 的签名 - CSDN](https://blog.csdn.net/chichoxian/article/details/95767768)
* [SignatureTools - GitHub](https://github.com/DeMonJavaSpace/SignatureTools)
* [Android 新版 v2 签名&渠道包工具 - CSDN](https://blog.csdn.net/DeMonliuhui/article/details/109455135)
* [细说 Android apk 四代签名 - 腾讯云](https://cloud.tencent.com/developer/article/1916927)

## 2022-05-18 星期三

### Sublime Text 2

* [Sublime Text 2 - Show file navigation in sidebar - stackoverflow](https://stackoverflow.com/questions/11995591/sublime-text-2-show-file-navigation-in-sidebar)

* [Highlight currently open file in the project tree - Sublime Forum](https://forum.sublimetext.com/t/highlight-currently-open-file-in-the-project-tree/10306)

在侧边栏中显示当前打开的文件：打开 `Preferences -> Key Bindings`，加入以下内容，保存退出。

```js
{ "keys": ["ctrl+alt+s"], "command": "reveal_in_side_bar" },
```



## 2022-05-11 星期三

### Android 代码裁剪

* [裁剪、混淆和优化你的应用 - Android Developers](https://developer.android.com/studio/build/shrink-code)

```groovy
android {
    buildTypes {
        release {
            // Enables code shrinking, obfuscation, and optimization for only
            // your project's release build type.
            minifyEnabled true

            // Enables resource shrinking, which is performed by the
            // Android Gradle plugin.
            shrinkResources true

            // Includes the default ProGuard rules files that are packaged with
            // the Android Gradle plugin. To learn more, go to the section about
            // R8 configuration files.
            proguardFiles getDefaultProguardFile(
                    'proguard-android-optimize.txt'),
                    'proguard-rules.pro'
        }
    }
    ...
}
```

### UE4 Android WebView

* [UE4 内嵌 Web - Goulandis](https://goulandis.github.io/2021/05/14/%E3%80%90UE4%E3%80%91UE4%E5%86%85%E5%B5%8CWeb%E5%8F%8A%E4%B8%8EWeb%E9%80%9A%E4%BF%A1/#)

### UE4 Android HTTP

* [UE 开发笔记：Android 篇 - imzlp](https://imzlp.com/posts/17996/)

![image-20220517201055094](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220517201055094.png)

* [Network Security Configuration File - Unreal Engine Forums](https://forums.unrealengine.com/t/network-security-configuration-file/139286)

## 2022-04-28 星期四

### Android 渠道包

* [开源 Android 渠道包生成工具 Walle - 美团技术团队](https://tech.meituan.com/2017/01/13/android-apk-v2-signature-scheme.html)
* [walle - GitHub](https://github.com/Meituan-Dianping/walle)
* [Android 多渠道打包的三种方式 - CSDN](https://blog.csdn.net/mayn666/article/details/79878469)
* [Android 多渠道打包（相同工程不同包名等）- 简书](https://www.jianshu.com/p/9bfc4b23b2c0)

## 2022-04-21 星期四

### UE4 的光照与阴影

* [Unreal Engine 4 的光与影 - Unreal Engine Blog](https://www.unrealengine.com/zh-CN/blog/chn-unreal-engine-4-light-and-shadow?sessionInvalidated=true)

![02.png](media/PRG-0008-A-Game-Development-Blackboard-Part-3/Unreal+Engine%252Fblog%252Fchn-unreal-engine-4-light-and-shadow%252F02-2063x783-fa4f00db9d0035b35baa5e7c51403e02694b04db.png)

## 2022-04-11 星期一

### UE4 资源管理

* [UE4 的资源管理 - 知乎](https://zhuanlan.zhihu.com/p/357904199)

> 资源的卸载
> 默认情况下，加载中的资源由引擎持有引用，不会被卸载，加载完成后的资源会依赖引擎的gc卸载。如果没有被使用到，会在下次gc的时候释放掉。如果需要立即释放可以手动强制引擎gc。
>
> 但是可能有时候由于内存或其他各种原因，只想立即释放掉指定资源的内存，不想调用全局gc导致游戏产生卡顿，这时候要怎么办呢？我查了引擎官方文档以及网上各种文章，基本没有明确给出答案，下面我会根据以往我的经验介绍一些做法（野路子），不代表正确，但实测确实能立即释放掉内存，只是要自己额外花一些功夫保证安全。
>
> * 大部分UObject，可以手动调用ConditionalBeginDestory，这里会主动先把对象的资源清理掉，留下一个空壳UObject。可以看引擎源码，这个函数相当于主动调用BeginDestroy，在对象gc时候也会调用，但是因为是Conditional的，如果之前已经调用过，在gc的时候就不会再次调用BeginDestroy从而避免了逻辑错误。通过这种方式，业务需要自行保证对象不再被使用，否则会出BUG。
> * 如果是贴图，材质或Mesh等资源，可以直接调用ReleaseResource，这里内部会先把贴图或网格内存先释放，执行结束之后留下一个空壳UObject，对于空壳UObject其实就不怎么占用内存了，等待gc的时候销毁即可。另外因为有的ReleaseResource会Flush渲染命令队列可能产生卡顿，所以可以尽量把ReleaseResource这个函数提交到渲染命令队列，虽然内存释放不那么及时，但也比gc快很多，大部分情况一帧内就会释放掉。通过这种方式，业务也需要自行保证对象不再被使用，否则会出BUG。
> * 如果是RenderTarget，引擎有提供专门的池，可以回收复用。
> * 如果是动态材质，也有专门的函数可以删除。
> * 如果是Actor或ActorComponent等，有专门的删除函数，可以调用DestroyActor或DestroyComponent，基本上能释放掉大部分资源。对于SceneComponent可以主动调用DestroyPhysicsState和DestroyRenderState释放掉物理或场景中的对象，也能立即释放一些内存。

## 2022-02-21 星期一

### 游戏安全

* [深入解析 Lua 脚本加密技术，提升游戏代码的安全性](https://dun.163.com/news/p/ab38146da80b4a6a9b689729f62ce1ea)

### macOS 安全设置

* [macOS 允许任何来源的 App - 知乎](https://zhuanlan.zhihu.com/p/51328476)

```sh
sudo spctl --master-disable
```

### UE4 Editor Splash

* [Editor Splash screen customisation - Unreal Engine Forums](https://forums.unrealengine.com/t/editor-splash-screen-customisation/624)

> /Engine/Content/Splash/EdSplash.bmp

## 2022-02-08 星期二

### UE4 内存分配器

* [UE4 MallocBinned2 分配器 - 知乎](https://zhuanlan.zhihu.com/p/79715624)
* [UE4 MallocBinned 分配器 - 知乎](https://zhuanlan.zhihu.com/p/393382059)

### C/C++ 内存错误检测器

* [AddressSanitizer - GitHub](https://github.com/google/sanitizers/wiki/AddressSanitizer)

> [Build Configuration - UE Documentation](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/BuildTools/UnrealBuildTool/BuildConfiguration/)
>
> **bEnableAddressSanitizer**: Enables address sanitizer (ASan)

## 2022-01-16 星期日

### Logcat window missing from Android Stuido

* [Logcat Missing from Android Studio - stackoverflow](https://stackoverflow.com/questions/51381604/logcat-missing-from-android-studio-3-1-3)

> 1. Go to File > Open
> 2. Select the folder with the 'app' folder inside your project
> 3. Press 'Open'

### 批处理文件操作

* [bat：删除部分文件和文件夹，仅保留指定文件和文件夹 - CSDN](https://blog.csdn.net/shijianduan1/article/details/105718813)

## 2022-01-10 星期一

### UE4 D3D11RHI Crash Fix

Standalone 模式下，加载某个关卡时，必定崩溃，日志如下：

```
LogWindows: Error: Error reentered: Assertion failed: EnumHasAllFlags(Pipeline, AllowedSrc) [File:E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Public\RHI.h] [Line: 1989] 
Transition is being used on a source pipeline that it wasn't created for.
LogThreadingWindows: Error: Runnable thread RenderThread 1 crashed.
LogWindows: Error: === Critical error: ===
LogWindows: Error: 
LogWindows: Error: Fatal error: [File:E:/Epic Games/UE_4.26/Engine/Source/Runtime/Windows/D3D11RHI/Private/D3D11Commands.cpp] [Line: 1444] 
LogWindows: Error: Null SRV (resource 0 bind 2) on UB Layout FInstancedStaticMeshVertexFactoryUniformShaderParameters
LogWindows: Error: 
LogWindows: Error: 
LogWindows: Error: [Callstack] 0x00007fff4aa94f69 KERNELBASE.dll!UnknownFunction []
LogWindows: Error: [Callstack] 0x00007ffec1759af6 UE4Editor-Core.dll!ReportAssert() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Windows\WindowsPlatformCrashContext.cpp:1616]
LogWindows: Error: [Callstack] 0x00007ffec175d489 UE4Editor-Core.dll!FWindowsErrorOutputDevice::Serialize() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Windows\WindowsErrorOutputDevice.cpp:78]
LogWindows: Error: [Callstack] 0x00007ffec147528d UE4Editor-Core.dll!FOutputDevice::LogfImpl() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Misc\OutputDevice.cpp:61]
LogWindows: Error: [Callstack] 0x00007ffead94a67a UE4Editor-D3D11RHI.dll!SetShaderResourcesFromBuffer_SRV<0>() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Windows\D3D11RHI\Private\D3D11Commands.cpp:1448]
LogWindows: Error: [Callstack] 0x00007ffead9491e7 UE4Editor-D3D11RHI.dll!FD3D11DynamicRHI::SetResourcesFromTables<FD3D11VertexShader>() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Windows\D3D11RHI\Private\D3D11Commands.cpp:1567]
LogWindows: Error: [Callstack] 0x00007ffead95b9a3 UE4Editor-D3D11RHI.dll!FD3D11DynamicRHI::CommitGraphicsResourceTables() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Windows\D3D11RHI\Private\D3D11Commands.cpp:1643]
LogWindows: Error: [Callstack] 0x00007ffead980aec UE4Editor-D3D11RHI.dll!FD3D11DynamicRHI::RHIDrawIndexedPrimitive() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Windows\D3D11RHI\Private\D3D11Commands.cpp:1752]
LogWindows: Error: [Callstack] 0x00007ffec0f0d971 UE4Editor-RHI.dll!FRHICommandDrawIndexedPrimitive::Execute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Public\RHICommandListCommandExecutes.inl:203]
LogWindows: Error: [Callstack] 0x00007ffeb08e45e2 UE4Editor-Renderer.dll!FRHICommand<FRHICommandDrawIndexedPrimitive,FRHICommandDrawIndexedPrimitiveString1015>::ExecuteAndDestruct() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Public\RHICommandList.h:763]
LogWindows: Error: [Callstack] 0x00007ffec0f17a95 UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteInner_DoExecute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:368]
LogWindows: Error: [Callstack] 0x00007ffec0f174c4 UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteInner() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:659]
LogWindows: Error: [Callstack] 0x00007ffec0f1818c UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteList() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:682]
LogWindows: Error: [Callstack] 0x00007ffec0f0faf7 UE4Editor-RHI.dll!FRHICommandWaitForAndSubmitSubList::Execute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:1109]
LogWindows: Error: [Callstack] 0x00007ffec0f152f5 UE4Editor-RHI.dll!FRHICommand<FRHICommandWaitForAndSubmitSubList,FRHICommandWaitForAndSubmitSubListString1075>::ExecuteAndDestruct() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Public\RHICommandList.h:763]
LogWindows: Error: [Callstack] 0x00007ffec0f17a95 UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteInner_DoExecute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:368]
LogWindows: Error: [Callstack] 0x00007ffec0f174c4 UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteInner() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:659]
LogWindows: Error: [Callstack] 0x00007ffec0f187c5 UE4Editor-RHI.dll!FRHICommandListExecutor::ExecuteList() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:709]
LogWindows: Error: [Callstack] 0x00007ffec0f0aea2 UE4Editor-RHI.dll!FRHICommandList::EndScene() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RHI\Private\RHICommandList.cpp:1575]
LogWindows: Error: [Callstack] 0x00007ffeb0f81160 UE4Editor-Renderer.dll!TRDGLambdaPass<FEmptyShaderParameters,<lambda_07b80eccfb5e773bbe1f3ce853d577a8> >::ExecuteImpl() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Public\RenderGraphPass.h:424]
LogWindows: Error: [Callstack] 0x00007ffed14a5509 UE4Editor-RenderCore.dll!FRDGPass::Execute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Private\RenderGraphPass.cpp:302]
LogWindows: Error: [Callstack] 0x00007ffed14a92ba UE4Editor-RenderCore.dll!FRDGBuilder::ExecutePass() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Private\RenderGraphBuilder.cpp:1593]
LogWindows: Error: [Callstack] 0x00007ffed14a4ab3 UE4Editor-RenderCore.dll!FRDGBuilder::Execute() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Private\RenderGraphBuilder.cpp:1253]
LogWindows: Error: [Callstack] 0x00007ffeb099a751 UE4Editor-Renderer.dll!FDeferredShadingSceneRenderer::Render() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Renderer\Private\DeferredShadingRenderer.cpp:2618]
LogWindows: Error: [Callstack] 0x00007ffeb0fa4b3b UE4Editor-Renderer.dll!RenderViewFamily_RenderThread() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Renderer\Private\SceneRendering.cpp:3619]
LogWindows: Error: [Callstack] 0x00007ffeb0f5a8ef UE4Editor-Renderer.dll!<lambda_3e02a5f531a5d4cb7f869072a107ef0b>::operator()() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Renderer\Private\SceneRendering.cpp:3889]
LogWindows: Error: [Callstack] 0x00007ffeb0f7e78d UE4Editor-Renderer.dll!TEnqueueUniqueRenderCommandType<`FRendererModule::BeginRenderingViewFamily'::`35'::FDrawSceneCommandName,<lambda_3e02a5f531a5d4cb7f869072a107ef0b> >::DoTask() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Public\RenderingThread.h:183]
LogWindows: Error: [Callstack] 0x00007ffeb0f827c3 UE4Editor-Renderer.dll!TGraphTask<TEnqueueUniqueRenderCommandType<`FRendererModule::BeginRenderingViewFamily'::`35'::FDrawSceneCommandName,<lambda_3e02a5f531a5d4cb7f869072a107ef0b> > >::ExecuteTask() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Public\Async\TaskGraphInterfaces.h:886]
LogWindows: Error: [Callstack] 0x00007ffec1215e34 UE4Editor-Core.dll!FNamedTaskThread::ProcessTasksNamedThread() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Async\TaskGraph.cpp:709]
LogWindows: Error: [Callstack] 0x00007ffec121623e UE4Editor-Core.dll!FNamedTaskThread::ProcessTasksUntilQuit() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Async\TaskGraph.cpp:601]
LogWindows: Error: [Callstack] 0x00007ffed14cb0d2 UE4Editor-RenderCore.dll!RenderingThreadMain() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Private\RenderingThread.cpp:373]
LogWindows: Error: [Callstack] 0x00007ffed14d37a4 UE4Editor-RenderCore.dll!FRenderingThread::Run() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\RenderCore\Private\RenderingThread.cpp:509]
LogWindows: Error: [Callstack] 0x00007ffec176bb2b UE4Editor-Core.dll!FRunnableThreadWin::Run() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Windows\WindowsRunnableThread.cpp:86]
LogWindows: Error: [Callstack] 0x00007ffec17678f7 UE4Editor-Core.dll!FRunnableThreadWin::GuardedRun() [E:\Epic Games\UE_4.26\Engine\Source\Runtime\Core\Private\Windows\WindowsRunnableThread.cpp:35]
LogWindows: Error: [Callstack] 0x00007fff4cb67034 KERNEL32.DLL!UnknownFunction []
LogWindows: Error: [Callstack] 0x00007fff4d162651 ntdll.dll!UnknownFunction []
LogWindows: Error: 
LogWindows: Error: Crash in runnable thread RenderThread 1
```

查阅 UDN 上的相似的问题，[Crash from FD3D11DynamicRHI / SetShaderResourcesFromBuffer_SRV - UDN](https://udn.unrealengine.com/s/question/0D54z00007Ahw5tCAB/crash-from-fd3d11dynamicrhi-setshaderresourcesfrombuffersrv)，回答中提到可以尝试开启 RHI 线程；经过实际尝试后，并未能修复该 crash。

最终修复该 crash 的，是以下问题中提到的，在 UE 4.26 中存在的 bug，然后在 UE 4.27 中被修复。

* [HISM causes crash in build/standalone on reload level - UE4 ANSWERHUB](https://answers.unrealengine.com/questions/1002738/hism-causes-crash-in-buildstandalone-on-reload-lev.html)
* [Crash when spawning multiple HISM at runtime in a packaged shipping build - Unreal Engine Issues](https://issues.unrealengine.com/issue/UE-109511)
* [UnrealEngine - GitHub](https://github.com/EpicGames/UnrealEngine/commit/d19c69784b3160cbd0c0ddf77237f14ed64dba39)

![image-20220111163251902](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220111163251902.png)

### UE4 并行渲染

* [Parallel Rendering Overview - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/Rendering/ParallelRendering/)

## 2021-12-31 星期五

### UE4 Android Debugging

* [Android Debugging - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/AndroidDebugging/)
* [UE4 Android 联机调试 - 知乎（亲测可行）](https://zhuanlan.zhihu.com/p/46089199)
* [UE4 Android Studio 调试 - 博客园](https://www.cnblogs.com/kekec/p/12632422.html)

### Visual Studio Tips and Tricks

* [Visual Studio Tips and Tricks - UE Documentation](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/VisualStudioTipsAndTricks/)

> **Fixing the Configuration Combobox Width**
>
> The default solution configuration combobox is too small to see the full name of the option currently selected. To fix that, right-click on the **toolbar**, select **Customize**, select the **Commands** tab, select the **radio Toolbar > Standard**, scroll down to the **Solution Configurations**, click on **Modify Selection**, and put in the width you would like. A width of 200 is typically useful.

![Fixing the configuration combobox](media/PRG-0008-A-Game-Development-Blackboard-Part-3/combobox.jpg)

## 2021-12-28 星期二

### UE4 Device Profiles and Scalability

> Scalability settings define levels of quality for individual features like shadows, foliage, and mesh detail, condensing an array of different settings into one easily scaled value. Device profiles then map those settings to devices that are compatible with them.

* [Setting Device Profiles - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/DeviceProfiles/)
* [Mobile Performance Tips and Tricks - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Performance/TipsAndTricks/)
* [Performance Guidelines for Mobile Devices - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Performance/)
* [Configuration Files - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/ConfigurationFiles/)
* [Android Configuration Rules System - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/AndroidConfigRulesSystem/)
* [Customizing Device Profiles and Scalability for Android - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/CustomizingDeviceProfiles/)
* [iOS Device Compatibility - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/DeviceCompatibility/)

* [Scalability and The Developer - UE Documentation](https://docs.unrealengine.com/4.27/en-US/TestingAndOptimization/PerformanceAndProfiling/Scalability/ScalabilityAndYou/)
* [Scalability Reference - UE Documentation](https://docs.unrealengine.com/4.27/en-US/TestingAndOptimization/PerformanceAndProfiling/Scalability/ScalabilityReference/)

### UE4 开启 Cook 调试信息

![image-20211228181523927](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211228181523927.png)

![image-20211228181701612](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211228181701612.png)

![image-20211228181830957](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211228181830957.png)

## 2021-12-15 星期三

### Building Unreal Engine from Source

* [Building Unreal Engine from Source - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DevelopmentSetup/BuildingUnrealEngine/)
* [从源码构建虚幻引擎](http://docs.manew.com/ue4/775.html)
* [Versioning of Binaries - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/BuildTools/UnrealBuildTool/VersioningofBinaries/)
* [Compiling Game Projects - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DevelopmentSetup/CompilingProjects/)

### Making an Unreal Engine Installed Build

* [Using an Installed Build - UE Documentation](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DeployingTheEngine/UsinganInstalledBuild/)
* [BuildGraph Usage - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/BuildTools/AutomationTool/BuildGraph/Usage/)
* [Need VS 2017 to build plugins in 4.25? - UE4 AnswerHub](https://forums.unrealengine.com/t/need-vs-2017-to-build-plugins-in-4-25/469289)
* [BuildGraph：构建支持多平台打包的二进制引擎 - 循迹研究室](https://imzlp.com/posts/11956/)

![image-20211221215941432](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211221215941432.png)

修改 `Engine/Build/InstalledEngineBuild.xml`，找到 `Compile UE4Game Win64` 节点，移除 `-allmodules` 和 `-nolink` 选项，以加快编译速度。

```shell
# 需要安装并使用 Visual Studio 2017 来构建 Installed Build
cd Engine\Build\BatchFiles
.\RunUAT.bat BuildGraph -target="Make Installed Build Win64" -script="Engine/Build/InstalledEngineBuild.xml" -set:WithWin32=false -set:WithLinux=false -set:WithLinuxAArch64=false -set:WithAndroid=false -set:WithHoloLens=false -set:WithLumin=false -set:WithMac=false -set:WithIOS=false -set:WithTVOS=false -set:WithLuminMac=false -set:WithDDC=false -set:GameConfigurations=Development

.\RunUAT.bat BuildGraph -target="Make Installed Build Win64" -script="Engine/Build/InstalledEngineBuild.xml" -set:WithWin32=false -set:WithLinux=false -set:WithLinuxAArch64=false -set:WithAndroid=true -set:WithHoloLens=false -set:WithLumin=false -set:WithMac=false -set:WithIOS=false -set:WithTVOS=false -set:WithLuminMac=false -set:WithDDC=false
```

* [Unreal Binary Builder - GitHub](https://github.com/ryanjon2040/Unreal-Binary-Builder)

### Derived Data Cache

* [Derived Data Cache - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DerivedDataCache/)
* [Windows 共享文件夹设置无密码访问 - CSDN](https://blog.csdn.net/u013992330/article/details/104864422)
* [Windows Guest 无密码共享 - 简书](https://www.jianshu.com/p/f11e075b415c)

### Develop UE4 Games on Mac

* [ue4-xcode-vscode-mac - GitHub](https://github.com/botman99/ue4-xcode-vscode-mac)

### dos2unix

* [Dos2Unix / Unix2Dos - Text file format converters](https://waterlan.home.xs4all.nl/dos2unix.html)

```shell
PS D:\dos2unix-7.4.2-win64\bin> get-childitem -path . -filter '*.sh' -recurse | foreach-object {.\dos2unix.exe $_.Fullname}
```

### UE4 断言

* [UE4 断言总结 - 知乎](https://zhuanlan.zhihu.com/p/64462945)

> 1. 停止执行 (check族)
> 表达式为false即立刻中断，引擎崩溃
> 2. Debug(DO_GUARD_SLOW=1)时停止执行 (checkSlow族)
> 仅在Debug模式下崩溃
> 3. 不停止执行 (ensure族)
> 不会中断 但会生成callstack报告供debug
> ensure会返回bool型结果

### UE 4.26 Android Crash on "/apex/com.android.runtime/lib/bionic/libc.so"

> D/UE4(17975): Ensure condition failed: GetShadowIndex() == 0 [File:E:/Epic Games/UE_4.26.2/Engine/Source/Runtime/Core/Public\HAL/IConsoleManager.h] [Line: 1296]

```c++
// IConsoleManager.h
// faster than GetValueOnAnyThread()
T GetValueOnGameThread() const
{
	// compiled out in shipping for performance (we can change in development later), if this get triggered you need to call GetValueOnRenderThread() or GetValueOnAnyThread(), the last one is a bit slower
	cvarCheckCode(ensure(GetShadowIndex() == 0));	// ensure to not block content creators, #if to optimize in shipping
	return ShadowedValue[0];
}
```

* [Application crash on android when switching from the game level to the main menu level - UE4 AnswerHub](https://answers.unrealengine.com/questions/1005324/application-crash-on-android-when-switching-from-t.html?sort=oldest)

```ini
;BaseEngine.ini
gc.MultithreadedDestructionEnabled=False
```

### SVN 上传 .so  .a .o 文件

* [SVN 上传不了 .so .a 库可尝试的解决方法 - CSDN](https://blog.csdn.net/brlf_gz/article/details/78402755?spm=1001.2014.3001.5501)

### SVN 递归忽略指定目录

* [Ignore some directories recursively - stackoverflow](https://stackoverflow.com/questions/2035335/svn-ignore-some-directories-recursively)
* [How do I ignore files in SVN? - stackoverflow](https://stackoverflow.com/questions/86049/how-do-i-ignore-files-in-subversion)

> SVN 不区分文件和文件夹，符合规则的文件和目录都会被忽略，但不能对已添加过版本控制的文件进行忽略。

### SVN Cleanup 失败修复方法

* [solution of svn run cleanup failed](https://www.anujvarma.com/svn-cleanup-failedprevious-operation-has-not-finished-run-cleanup-if-it-was-interrupted/)

> 1. Install sqllite
>
> 2. sqlite3 .svn/wc.db “select * from work_queue”
>
> The SELECT should show you your offending folder/file as part of the work queue. What you need to do is delete this item from the work queue.
>
> 3. sqlite3 .svn/wc.db “delete from work_queue”

## 2021-12-12 星期日

### Android Device Monitor

* [Android Device Monitor - Android Developers](https://developer.android.com/studio/profile/monitor)

> 位于 android-sdk/tools/ 目录下

### UE4 Android Error "Failed to open descriptor file xxx.uproject" or "Project file not found: xxx.uproject"

* 可能为缺少 “访问内部存储” 或 “访问所有文件” 权限
* ["Failed to open descriptor file" error with Android target SDK 29 - UE4 AnswerHub](https://answers.unrealengine.com/questions/974736/view.html)
* [Android 权限大全 - 博客园](https://www.cnblogs.com/classic/archive/2011/06/20/2085055.html)
* [“所有文件访问权限”的使用 - Play 管理中心帮助](https://support.google.com/googleplay/android-developer/answer/10467955?hl=zh-Hans)

```ini
android:requestLegacyExternalStorage="true"

android.permission.MANAGE_EXTERNAL_STORAGE
```

![image-20211217212223446](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211217212223446.png)

### UE4 应用的启动流程

* [Unreal Engine 的启动流程 - 知乎](https://zhuanlan.zhihu.com/p/610523485)
* [Android 启动流程 - 知乎](https://zhuanlan.zhihu.com/p/31892319)

## 2021-11-11 星期四

### 代码静态检查工具

* [TscanCode - GitHub](https://github.com/Tencent/TscanCode)

### UE4 中的 C++ 对象类型检查

* [Best way to check class type in C++? - UE4 ANSWERHUB](https://answers.unrealengine.com/questions/660033/best-way-to-check-class-type-in-c.html)

```c++
if(myGrabbedItem->IsA(ABaseWeapon::StaticClass()))
{
    this->GrabWeapon(myGrabbedItem);
}
else
{
    this->GrabItem(myGrabbedItem);
}
```

## 2021-11-05 星期五

### UE4 Android Packaging

* [Setting Up Android SDK and NDK for Unreal - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/Setup/AndroidStudio/)
* [NDK Downloads - Android Developers](https://developer.android.com/ndk/downloads)
* [Packaging Android Projects - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
* [Reducing Packaged Game Size - UE Documentation](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/PerformanceAndProfiling/ReducingPackageSize/)
* [Reducing APK Package Size - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/ReducingAPKSize/)
* [游戏打包 - 知乎](https://zhuanlan.zhihu.com/p/60996027)
* [如何完全卸载 Android Studio - CSDN](https://blog.csdn.net/qq_33721320/article/details/114977456)
* [Android Gradle plugin release notes - Android Developers](https://developer.android.google.cn/studio/releases/gradle-plugin)

### UE4 Android Packaging 工具链版本设置

#### NDK Version

> `C:\Users\[USERNAME]\AppData\Local\Android\Sdk\ndk\21.4.7075529`

![image-20220510194347481](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510194347481.png)

![image-20220510194625248](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510194625248.png)

> ..\Engine\Programs\AutomationTool\Saved\Logs\UBT-[PROJECT_NAME]-Android-Development.txt

```
AndroidPlatform.SetUpSpecificEnvironment: PLATFORM_ANDROID_NDK_VERSION = 210500
AndroidPlatform.SetUpSpecificEnvironment: NDK toolchain: r21e, NDK version: 30, GccVersion: 4.9, ClangVersion: 9.0.9
```

#### NDK API Level

> C:\Users\[USERNAME]\AppData\Local\Android\Sdk\ndk\21.4.7075529\platforms

![image-20220510200535345](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510200535345.png)

> ..\Engine\Programs\AutomationTool\Saved\Logs\UBT-[PROJECT_NAME]-Android-Development.txt

```
AndroidPlatform.SetUpSpecificEnvironment: PLATFORM_ANDROID_NDK_VERSION = 210500
AndroidPlatform.SetUpSpecificEnvironment: NDK toolchain: r21e, NDK version: 30, GccVersion: 4.9, ClangVersion: 9.0.9
```

#### SDK Build-Toos Version

> C:\Users\[USERNAME]\AppData\Local\Android\Sdk\build-tools\30.0.3

![image-20220510200925849](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510200925849.png)

![image-20220510201245759](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510201245759.png)

> ..\Engine\Programs\AutomationTool\Saved\Logs\UBT-[PROJECT_NAME]-Android-Development.txt

```
UEDeployAndroid.GetSdkApiLevel: Building Java with SDK API level 'android-31'
UEDeployAndroid.GetBuildToolsVersion: Building with Build Tools version '30.0.3'
```

#### SDK API Level

> C:\Users\[USERNAME]\AppData\Local\Android\Sdk\platforms\android-31

![image-20220510201652277](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510201652277.png)

![image-20220510201742944](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510201742944.png)

> ..\Engine\Programs\AutomationTool\Saved\Logs\UBT-[PROJECT_NAME]-Android-Development.txt

```
UEDeployAndroid.GetSdkApiLevel: Building Java with SDK API level 'android-31'
UEDeployAndroid.GetBuildToolsVersion: Building with Build Tools version '30.0.3'
```

#### Target SDK Version

![image-20220510202613823](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20220510202613823.png)

> ..\Engine\Programs\AutomationTool\Saved\Logs\UBT-[PROJECT_NAME]-Android-Development.txt

```
AndroidPlatform.Package: Target SDK Version 29
```

#### Android Gradle Plugin(AGP) Version & Gradle Version

AGP Version 与 Gradle Version 应兼容匹配，详见：[Android Gradle plugin release notes - Android Developers](https://developer.android.google.cn/studio/releases/gradle-plugin)

```c++
class UEDeployAndroid : UEBuildDeploy, IAndroidDeploy
{
    //...
	// classpath of default android build tools gradle plugin
	private const string ANDROID_TOOLS_BUILD_GRADLE_VERSION = "com.android.tools.build:gradle:4.0.0";   
    //...
}
```

UE4 的 AutomationTool 在 Make APK 时，实际上并不根据 AGP Version 确定最终使用的 Gradle Version，而是根据以下配置文件中的 `distributionUrl`，下载指定版本的 Gradle 并用于执行后续生成 APK 的工作。

> ..\Engine\Build\Android\Java\gradle\gradle\wrapper\gradle-wrapper.properties

```properties
#Tue Feb 04 16:06:19 EST 2020
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-6.1.1-all.zip
```

> ..\[PROJECT]\Intermediate\Android\arm64\gradle\\.gradle

#### UE4 默认的 Android 工具链版本

> ..\Engine\Extras\Android\SetupAndroid.bat

```bash
call "%SDKMANAGER%" "platform-tools" "platforms;android-28" "build-tools;28.0.3" "cmake;3.10.2.4988404" "ndk;21.4.7075529"
```

### UE4 iOS Packaging

* [iOS Quick Start - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/QuickStart/)
* [iOS Provisioning - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/Provisioning/)
* [Distribution on iOS - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/iOS/Distribution/)
* [UE4 打包 iOS 的两种方案 - 知乎](https://zhuanlan.zhihu.com/p/374158520)
* [Apple Developer](https://developer.apple.com/)
* [Remove obsolete mobile provision profiles - Unreal Engine Forums](https://forums.unrealengine.com/t/remove-obsolete-mobileprovision-profiles-ios/317570)

```sh
[Mac]
~/Library/MobileDevice/Provisioning Profiles
/Library/MobileDevice/Provisioning Profiles
```

* [iPhonePackager - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/iOS/iPhonePackager/)
* [UE 开发笔记：Mac/iOS 篇 - imzlp](https://imzlp.com/posts/1948/)
* [Using the Windows Metal Shader Compiler for iOS - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/WindowsMetalShader/)

### UE4 Patch

* [How to Create a Patch - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Patching/GeneralPatching/HowToCreatePatch/)

### HotPatcher

* [UE4 Plugin: HotPatcher - GitHub](https://github.com/hxhb/HotPatcher)
* [UE 热更新：需求分析与方案设计 - imzlp.com](https://imzlp.com/posts/17371/)
* [UE 资源热更打包工具 HotPatcher - imzlp.com](https://imzlp.com/posts/17590/)
* [UE 热更新：Questions & Answers - imzlp.com](https://imzlp.com/posts/16895/)
* [UE 热更新：拆分基础包 - imzlp.com](https://imzlp.com/posts/13765/)
* [UE 热更新：Shader 更新策略](https://imzlp.com/posts/15810/)

### UnrealPak

* [UnrealPak 与 Pak 的制作、挂载、加载 - 博客园](https://www.cnblogs.com/shiroe/p/14803859.html)
* [UE4 的 Pak 从打包到加载 - 知乎](https://zhuanlan.zhihu.com/p/340563727)

#### UE4 查看 pak 文件内容

* [UnrealPakViewer - GitHub](https://github.com/jashking/UnrealPakViewer)

## 2021-10-26 星期二

### 引擎中台

* [引擎中台助力《使命召唤手游》技术升级 - 腾讯游戏学堂](https://gameinstitute.qq.com/course/detail/10195)

![img](media/PRG-0008-A-Game-Development-Blackboard-Part-3/QMzhVw3UA9FX1o3ZuG75.jpg)

![img](media/PRG-0008-A-Game-Development-Blackboard-Part-3/Sl1T2Q1wvjfzluEpcIU5.jpg)

### 游戏工业化

* [2022 游戏工业化之战 - 知乎](https://zhuanlan.zhihu.com/p/479291088)

## 2021-10-10 星期日

### Support for Google Android App Bundle(AAB) in Unreal Engine

* [Customizable delivery with the App Bundle and easy sharing of test builds (Google I/O 19) - YouTube](https://youtu.be/flhib2krW7U)

* [Android App Bundle - Android Developers](https://developer.android.com/platform/technology/app-bundle)

  > Android App Bundle 是 Android 新推出的一种官方发布格式，可让您以更高效的方式开发和发布应用。借助 Android App Bundle，您可以更轻松地以更小的应用提供优质的使用体验，从而提升安装成功率并减少卸载量。转换过程轻松便捷。您无需重构代码即可开始获享较小应用的优势。改用这种格式后，您可以体验模块化应用开发和可自定义功能交付，并从中受益。

* [Android App Bundle 简介 - Android Developers](https://developer.android.com/guide/app-bundle)

![image-20211010173630604](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20211010173630604.png)

* [Play Asset Delivery - Android Developers](https://developer.android.com/guide/playcore/asset-delivery)

> Play Asset Delivery (PAD) 将 app bundle 的优势带到游戏中。它允许超过 150 MB 的游戏替换旧版扩展文件 (OBB)，方法是将包含游戏所需的所有资源的单个工件发布到 Play。PAD 提供了灵活的分发模式、自动更新、压缩和增量修补功能，并且可免费使用。使用 PAD，所有资源包均在 Google Play 上托管和提供，因此您无需使用内容分发网络 (CDN) 向玩家提供游戏资源。
>
> Play Asset Delivery 使用资源包，资源包由资源（如纹理、着色器和声音）组成，但不包含可执行代码。通过 Dynamic Delivery，您可以按照以下三种分发模式自定义如何以及何时将各个资源包下载到设备上：安装时分发、快速跟进式分发和按需分发。

> **下载大小上限**
>
> Asset Pack 因具有较高的大小上限而成为大型游戏的理想之选：
>
> 1. 每个 `fast-follow` 和 `on-demand` Asset Pack 的下载大小上限为 512 MB。
> 2. 所有 `install-time` Asset Pack 的总下载大小上限为 1 GB。
> 3. 一个 Android App Bundle 中的所有 Asset Pack 的总下载大小上限为 2 GB。
> 4. 一个 Android App Bundle 中最多可以使用 50 个资源包。

* [Play Feature Delivery 概览 - Android Developers](https://developer.android.com/guide/app-bundle/dynamic-delivery)
* [Build and test your Android App Bundle - Android Developers](https://developer.android.com/guide/app-bundle/test)
* [bundletool - Android Developers](https://developer.android.com/studio/command-line/bundletool)
* [Build your app from the command line - Android Developers](https://developer.android.com/build/building-cmdline#build_bundle)
* [啥是 Android App Bundle？- 知乎](https://zhuanlan.zhihu.com/p/61663559)

> * 资源选择性加载
> * 动态下发 lib

* [Packaging Android Projects - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
* [Google Play Asset Delivery Reference - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/Distribution/GooglePlayAssetDeliveryReference/)
* [Google Play Game's Asset Delivery - YouTube](https://youtu.be/WW9GevpEo1s)
* [Build error: "Installed Build Tools revision 31.0.0 is corrupted" - stackoverflow](https://stackoverflow.com/questions/68387270/android-studio-error-installed-build-tools-revision-31-0-0-is-corrupted)
* [Share app bundles and APKs internally - Play Console Help](https://support.google.com/googleplay/android-developer/answer/9844679)
* [Play Internal App Sharing URL - Google Play](https://play.google.com/console/internal-app-sharing/)
* [Inspect app versions with app bundle explorer - Play Console Help](https://support.google.com/googleplay/android-developer/answer/9844279)

## 2021-10-07 星期四

### Unreal Engine on GitHub

* [UE4 on GitHub - Unreal Engine](https://www.unrealengine.com/en-US/ue4-on-github?lang=en-US)

## 2021-09-27 星期一

### UE4 Derived Data Cache

* [Derived Data Cache - UE Documentation](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DerivedDataCache/)

## 2021-09-11 星期六

### UE4 Packaging C++ Macro define

* [How to add C++ macro define for android packaging - UE4 ANSWERHUB](https://answers.unrealengine.com/questions/380484/how-to-add-c-macro-define-for-android-packaging.html)

## 2021-08-25 星期三

### Wwise

* [Wwise 基础知识 - audiokinetic](https://www.audiokinetic.com/zh/public-library/2024.1.5_8803/?source=WwiseFundamentalApproach&id=wwise_fundamentals)
* [Wwise 音频解决方案概述 - 博客园](https://www.cnblogs.com/kekec/p/11714507.html)
* [UE4 中整合 Wwise - 知乎](https://zhuanlan.zhihu.com/p/41761623)
* [Wwise 快速上手指南：程序员篇（v2016.1）- 腾讯游戏学堂](https://gameinstitute.qq.com/community/detail/107700#)
* [示例 - audiokinetic](https://www.audiokinetic.com/zh/library/edge/?source=SDK&id=samplecode.html)
* [SoundBank 的管理策略 - audiokinetic](https://www.audiokinetic.com/zh/public-library/2024.1.5_8803/?source=Help&id=strategies_for_managing_soundbanks)
* [Wwise 中的 Game Object - AA Audio](http://jazzlost.me/2019/04/28/Game-Object-In-Wwise/)

**音频程序 blog**

* [AA Audio](http://jazzlost.me/)
* [FPS 项目声音设计框架 - AA Audio](http://jazzlost.me/2019/08/12/FPS-Project-Sound-Framework/)
* [《双生视界》的音频设计 - audiokinetic](https://blog.audiokinetic.com/zh/sound-design-of-girl-cafe-gun-2/)

## 2021-07-30 星期五

### UE4 编译原理

> 不要成为编译器的奴隶！

* [Build flow of the Unreal Engine 4 project](https://imzlp.com/posts/6362/)
* [UE4 中的反射之一：编译阶段 - 知乎](https://zhuanlan.zhihu.com/p/46836554)
* [从源码剖析虚幻引擎编译原理](https://yinpengd.github.io/2019/08/13/%E4%BB%8E%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90%E8%99%9A%E5%B9%BB%E5%BC%95%E6%93%8E%E7%BC%96%E8%AF%91%E5%8E%9F%E7%90%86/)
* [UE4 属性系统（反射）- 博客园](https://www.cnblogs.com/ghl_carmack/p/5698438.html)
* [编译器的工作过程 - 阮一峰](http://www.ruanyifeng.com/blog/2014/11/compiler.html)
* [UE4 如何编译 C++ - 简书](https://www.jianshu.com/p/393aeabae3d6)
* [Unreal Build System - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/UnrealBuildSystem/)
* [Build Configurations Reference - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DevelopmentSetup/BuildConfigurations/)

**Clang 编译器的报错信息有时候并非准确，会误导人！**

* [Template compilation error: 'X' does not refer to a value - stackoverflow](https://stackoverflow.com/questions/41222330/template-compilation-error-x-does-not-refer-to-a-value)

## 2021-07-22 星期四

### FF7R 动画技术

* [FF7R 动画技术笔记](https://blog.ch-wind.com/note-cedec2020-final-fantasy-vii-remake-animation/)

## 2021-07-12 星期一

### JetBrains IDE 的行长度限制修改

* [How can I set the line limit length for different types of files? - stackoverflow](https://stackoverflow.com/questions/21873543/how-can-i-set-the-line-limit-length-for-different-types-of-files)

![image-20210715150534753](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20210715150534753.png)

### UE4 编译日志乱码问题解决

* [UE4 编译时出现中文乱码问题 - CSDN](https://blog.csdn.net/netyeaxi/article/details/81206896)

## 2021-07-08 星期四

### UE4 动态加载 UObject

* [Dynamic Load Object](https://michaeljcole.github.io/wiki.unrealengine.com/Dynamic_Load_Object/)

### IsValid() vs IsValidLowLevel()

* [What's the diference between using TWeakObjectPtr or using UObject*? - UE4 Answerhub](https://answers.unrealengine.com/questions/48818/whats-the-difference-between-using-tweakobjectptr.html)
* [Discussion: The use of IsValidLowLevel - UE Forums](https://forums.unrealengine.com/t/discussion-the-ab-use-of-isvalidlowlevel/21795/3)

> In this circumstance, doing a simple pointer check was insufficient, and my game was crashing because the interior UObject data was already partially destroyed but the pointer was still valid.
>
> **I found that IsValidLowLevel() was the only way to verify the full integrity of the UObject.**
>
> I agree that in many cases this extra check is not necessary!
>
> You should use your own judgement as to whether you feel IsValidLowLevel() will help you or not.
>
> The main thing you can take away from this post of mine is that if you ever get inexplicable crashes with UObjects using only simple pointer validity checks, you should certainly try out IsValidLowLevel()
>
> Ever since my experience during the Beta, I chose to always be as safe as possible and do IsValidLowLevel() checks.
>
> I’ve had cases where doing this extra check has helped in multiplayer games with replicated proxies being passed via Server function, and people besides myself have also encountered this.

## 2021-06-30 星期三

### Android 应用 Crash 堆栈

* [Android Native Crash 捕获与解析 - 知乎](https://zhuanlan.zhihu.com/p/352651095)
* [Bugly Android 符号表](https://bugly.qq.com/docs/user-guide/symbol-configuration-android/?v=20200622202242)

### References in C++

* [Why don't I need to check if references are invalid/null? - stackoverflow](https://stackoverflow.com/questions/2524870/why-dont-i-need-to-check-if-references-are-invalid-null)

### Crash 定位与修复

* [What do you do when Unreal Editor crashes? - YouTube](https://youtu.be/TXZGIvpEhW8)

## 2021-06-21 星期一

### Unreal Engine 开发笔记

* [Unreal Engine 开发笔记 - 循迹研究室](https://imzlp.com/notes/ue/)

## 2021-06-03 星期四

### UE4 Delete C++ Class

* [Delete a specific C++ Class](https://www.orfeasel.com/deleting-a-c-class/)

> 1. Close Visual Studio
> 2. Close UE4 Editor
> 3. Remove the corresponding .cpp and .h file from your disk in explorer
> 4. Remove everything in the folder Binaries
> 5. Right click the .uproject file and click **Generate Visual Studio project Files**
> 6. Get back to your normal activity

## 2021-05-06 星期四

### Blueprint Best Practices

* [Blueprint Best Practices - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/BestPractices/index.html)

## 2021-04-24 星期六

### UE4 C++ Assert

* [Asserts - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/Assertions/index.html)
* [When should I use Check()? - UE Answers](https://answers.unrealengine.com/questions/418935/when-should-i-use-check.html)

## 2021-04-13 星期二

### UE4 C++ deprecated

* [UE4: Deprecating Symbols](https://blog.squareys.de/ue4-deprecating-symbols/)

```c++
/** Number of elements
 * @deprecated Use Size instead
 */
UPROPERTY(meta=(DeprecatedProperty, DeprecationMessage="Use Size instead."))
int32 Count_DEPRECATED;

/** @brief Get answer to everything
 * @deprecated Use GetEarth() and GetAnswer() instead.
 */
UFUNCTION(BlueprintPure, meta=(DeprecatedFunction,
    DeprecationMessage="Use GetEarth() and GetAnswer() instead."))
int GetAnswerToEverything() const {
    return 42;
}

UCLASS(Deprecated)
class UDEPRECATED_MyObject : public UObject {
    GENERATED_BODY()
    /* ... */
};

/* @deprecated This was removed in version XY */
UENUM()
enum class EMyEnum_DEPRECATED : uint32 {
    /* @deprecated This was removed in version XY */
    MyValue_DEPRECATED = 0,
    /* @deprecated This was removed in version XY */
    YourValue_DEPRECATED = 1,
    /* ... */
};

USTRUCT()
struct UE_DEPRECATED(4.20, "MyStruct is deprecated, use YourStruct instead.") FMyStruct {
    GENERATED_BODY()
    /* ... */

    UPROPERTY(meta=(Deprecated,
        DeprecationMessage="MyStruct is deprecated, use YourStruct instead."))
    FString Name_DEPRECATED;
};

UE_DEPRECATED(4.20, "Use bar() instead.")
virtual void foo();
```

* [C++ attribute: deprecated](https://en.cppreference.com/w/cpp/language/attributes/deprecated)

```c++
#include <iostream>
 
[[deprecated]]
void TriassicPeriod() {
    std::clog << "Triassic Period: [251.9 - 208.5] million years ago.\n";
}
 
[[deprecated("Use NeogenePeriod() instead.")]]
void JurassicPeriod() {
    std::clog << "Jurassic Period: [201.3 - 152.1] million years ago.\n";
}
 
[[deprecated("Use calcSomethingDifferently(int).")]]    
int calcSomething(int x) {
    return x * 2;
}
 
int main()
{
    TriassicPeriod();
    JurassicPeriod();
}
```

## 2021-04-10 星期六

### UE4 C++ include

* [pragma once - Wikipedia](https://en.wikipedia.org/wiki/Pragma_once)

> In the C and C++ programming languages, pragma once is a non-standard but widely supported preprocessor directive designed to cause the current source file to be included only once in a single compilation.

### UE4 IWYU(Include-What-You-Use)

* [IWYU - UE4 Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/BuildTools/UnrealBuildTool/IWYU/index.html)

> When writing IWYU code, there are four specific conventions that we adopt:
>
> 1. **All header files include their required dependencies.**
> 2. **.cpp files include their matching \*.h files first.**
> 3. **PCH files are no longer explicitly included.**
> 4. **Monolithic header files are no longer included.**
>
> If you want your game to opt-in to IWYU, there are a few tips to keep in mind:
>
> 1. Include `CoreMinimal.h` at the top of each header file.
> 2. To verify that all of your source files include all of their required dependencies, compile your game project in non-unity mode with PCH files disabled.
> 3. If you need to access **UEngine** or **GEngine**, which are defined in `Runtime\Engine\Classes\Engine\Engine.h`, you can `#include Engine/Engine.h` (distinguishing from the monolithic header file, which is located at `Runtime\Engine\Public\Engine.h`).
> 4. If you use a class that the compiler doesn't recognize, and don't know what you need to include may be missing the header file. This is especially the case if you are converting from non-IWYU code that compiled correctly. You can look up the class in the API Documentation, and find the necessary modules and header files at the bottom of the page.

### UE4 C++ Forward Declaration 前置声明

* [Forward Declarations](https://nerivec.github.io/old-ue4-wiki/pages/forward-declarations.html)

> Using Forward Declarations you can have as many inter-relating classes as you want in your c++ code without having circular dependencies.

### region and endregion pragma

* [region and endregion pragma - Microsoft Documentation](https://docs.microsoft.com/en-us/cpp/preprocessor/region-endregion)

> `#pragma region` lets you specify a block of code that you can expand or collapse when using the outlining feature of the Visual Studio editor.

### TSubclassOf

* [TSubclassOf - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TSubclassOf/index.html)

> **TSubclassOf** is a template class that provides UClass type safety.

### UE4 UPROPERTY Access Modifiers

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/UE4AccessToVariables.jpg)

## 2021-04-06 星期二

### UE4 动态读写 DataTable

* [UE4 动态读写 DataTable 数据表 - 知乎](https://zhuanlan.zhihu.com/p/158714495)

### UE4 Plugin

* [Unreal Engine C++ Tutorial: Plugins - YouTube](https://youtu.be/mgFrFdzb7hg)
* [C++ Extending the Editor - YouTube](https://youtu.be/zg_VstBxDi8)

### UE4 C++ 单例

* [Unreal-style Singletons with Subsystems](https://benui.ca/unreal/subsystem-singleton/)
* [在虚幻引擎实现单例模式 - 知乎](https://zhuanlan.zhihu.com/p/57218085)
* [UE4SingletonDemo - GitHub](https://github.com/ReturnZero23/UE4SingletonDemo)
* [自定义单例类 - CSDN](https://blog.csdn.net/ttm2d/article/details/106441788)
* [error LNK2001: unresolved external symbol - stackoverflow](https://stackoverflow.com/questions/16049306/error-lnk2001-unresolved-external-symbol-private-static-class/28823331)

> The definition for a static data member shall appear in a namespace scope enclosing the member’s class definition.

### UE4 Log

* [Logs, Printing Messages To Yourself During Runtime](https://nerivec.github.io/old-ue4-wiki/pages/logs-printing-messages-to-yourself-during-runtime.html)
* [Custom Log Categories](https://blog.jamie.holdings/2020/04/21/unreal-engine-4-custom-log-categories/)

### UE4 Mac Build Log

`~/Library/Logs/Unreal\ Engine/LocalBuildLogs`

* `Log.txt`
* `UBT-UnrealPak-Mac-Development.txt`
* `UBT-ChessWar-IOS-Shipping.txt`

### UE4 Json

* [Json 用法汇总 - 知乎](https://zhuanlan.zhihu.com/p/74720067)

## 2021-04-01 星期四

### C++ 成员变量初始化

* [C++ initializing variables in header vs with constructor - stackoverflow](https://stackoverflow.com/questions/28413154/c-initializing-variables-in-header-vs-with-constructor)

## 2021-03-22 星期一

### UE4 C++ Programming

* [Introduction to C++ Programming in UE4](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/IntroductionToCPP/index.html)
* [Unreal Property System(Reflection) - UE Blog](https://www.unrealengine.com/zh-CN/blog/unreal-property-system-reflection)

### UE4 Actors

* [Actors - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/index.html)
* [Actors Lifecycle - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/ActorLifecycle/index.html)

![UE4 Actor LifeCycle](media/PRG-0008-A-Game-Development-Blackboard-Part-3/UE4ActorLifeCycle.png)

### UE4 字符串

* [String Handling - UE4 Documentation](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/)
* [Character Encoding - UE4 Documentation](https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/CharacterEncoding/)
* [FString - UE4 Documentation](https://docs.unrealengine.com/en-US/API/Runtime/Core/Containers/FString/index.html)
* [FString - UE API Reference](https://docs.unrealengine.com/en-US/API/Runtime/Core/Containers/FString/index.html)

### UE4 容器类

* [TArray - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TArrays/index.html)
* [TMap - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TMap/index.html)
* [TSet - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TSet/index.html)
* [UE4 容器的使用 - CSDN](https://blog.csdn.net/yangxuan0261/article/details/52078303)
* [Optimizing TArray Usage for Performance - UE Blog](https://www.unrealengine.com/en-US/blog/optimizing-tarray-usage-for-performance)

### UE4 Libraries

* [UE4 Libraries You Should Know About - UE Blog](https://www.unrealengine.com/zh-CN/blog/ue4-libraries-you-should-know-about)

> * *Engine\Source\Runtime\Core\Public\Containers\Array.h*
> * *Engine\Source\Runtime\Core\Public\Containers\Set.h*
> * *Engine\Source\Runtime\Core\Public\Containers\Map.h*
> * *Engine\Source\Runtime\Core\Public\Containers\UnrealString.h*
> * *Engine\Source\Runtime\Core\Public\UObject\NameTypes.h*
> * *Engine\Source\Runtime\Core\Public\Internationalization\Text.h*
> * *Engine\Source\Runtime\Core\Public\Math\UnrealMathUtility.h*
> * *Engine\Source\Runtime\Core\Public\GenericPlatform\GenericPlatformMath.h*

### UE4 Localization

* [Localization Overview - UE4 Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/Localization/Overview/index.html)

### UE4 智能指针

* [Unreal Smart Pointer Library - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/index.html)
* [Shared Pointers - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/SharedPointer/index.html)
* [Shared References - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/SharedReference/index.html)
* [Weak Pointers - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/WeakPointer/index.html)
* [UE4 智能指针](https://cloud.tencent.com/developer/article/1374075)
* [UE4 智能指针基础 - 知乎](https://zhuanlan.zhihu.com/p/94198883)

### UE4 GC 垃圾回收

* [UE4 对象内存管理几种模式 - 知乎](https://zhuanlan.zhihu.com/p/49046671)
* [UE4 内存管理实践 - CSDN](https://blog.csdn.net/yangxuan0261/article/details/52075581)
* [UE4 垃圾回收剖析 - 博客园](https://www.cnblogs.com/ghl_carmack/p/6112118.html)
* [Garbage Collection Overview](https://michaeljcole.github.io/wiki.unrealengine.com/Garbage_Collection_Overview/)
* [Garbage Collection & Dynamic Memory Alloction](https://michaeljcole.github.io/wiki.unrealengine.com/Garbage_Collection_&_Dynamic_Memory_Allocation/)
* [Garbage Collection: Count References to Any Object](https://michaeljcole.github.io/wiki.unrealengine.com/Garbage_Collection_~_Count_References_To_Any_Object/)

## 2021-03-06 星期六

### UE4 Networking

* [UE4 的 MMO 移动同步方案 - 知乎](https://zhuanlan.zhihu.com/p/352386027)

## 2021-02-06 星期六

### Movement in UE4

* [游戏角色的移动原理（上）- 游戏开发那些事](https://mp.weixin.qq.com/s?__biz=MzU4NDYwNDI2NQ==&mid=2247483959&idx=1&sn=6b48226aac96cd5b1972cf392f70c207&chksm=fd960d31cae1842724cbcb679e316873f1a60394397391484d71cded58a36e7101f82fc85c8e&mpshare=1&scene=1&srcid=0206gYidfI9o034qSpECGIXC&sharer_sharetime=1612598181454&sharer_shareid=247cb15e3482d664cd16d96b3a3f3f73&version=3.1.2.2211&platform=win#rd)
* [游戏角色的移动原理（下）- 游戏开发那些事](https://mp.weixin.qq.com/s?__biz=MzU4NDYwNDI2NQ==&mid=2247483960&idx=1&sn=b9f51039e0bc0376df576da948fc4d2b&chksm=fd960d3ecae18428b6d4d76db2658516b7f617b19deb3d1da8c0f7b91228c47f6a414da752bc&cur_album_id=1342928497043537921&scene=189#rd)

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/640)

* [RootMotion 详解 - 游戏开发那些事](https://mp.weixin.qq.com/s?__biz=MzU4NDYwNDI2NQ==&mid=2247483965&idx=1&sn=b731f781ffddbbd483f759790089cfbd&chksm=fd960d3bcae1842df3a4bd265bd68b2e911f603dbba0f858c18e2b7ddf7f9f160f7ec0e16f8c&cur_album_id=1342928497043537921&scene=189#rd)
* [How to achieve smooth rotation using Navmesh? - UE Answers](https://answers.unrealengine.com/questions/76200/view.html)

> Go to your AI Pawn and under Components > CharacterMovement > Enable "Orient Rotation to Movement"
>
> Then under Defaults > Pawn > Disable "Use Controller Rotation Yaw" & Under Character Movement > set "Yaw" to a value you like (for example 180).

### Navigation in UE4

Pawn 身上挂载的 Actor（比如武器），如其 Collision 设置不当，会导致 AI 的导航失效，从而导致 AI 寻路失败。 

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20210206212056955.png)

## 2021-02-04 星期四

### 函数参数前的 class 关键字

* [What is the class keyword before a function argument? - stackoverflow](https://stackoverflow.com/questions/35959438/what-is-the-class-keyword-before-a-function-argument/35959483)

### 函数声明后的 const 关键字

* [What is meant with const at end of function declaration? - stackoverflow](https://stackoverflow.com/questions/3141087/what-is-meant-with-const-at-end-of-function-declaration)

> A "const function", denoted with the keyword `const` after a function declaration, makes it a compiler error for this class function to change a member variable of the class. However, reading of a class variables is okay inside of the function, but writing inside of this function will generate a compiler error.

### UE4 C++ 文件中的宏

* [宏 GENERATED_UCLASS_BODY() 与 GENERATED_BODY() 简析 - CSDN](https://blog.csdn.net/xi_niuniu/article/details/50523928)

> 紧随 GENERATED_BODY() 之后的成员的默认访问方式为 private，而紧随 GENERATED_UCLASS_BODY() 之后的成员的默认访问方式为 public。
>
> GENERATED_BODY() 为我们生成默认构造函数，而 GENERATED_UCLASS_BODY() 为我们生成带有指定参数类型的构造函数。

### UE4 学习资料

#### 网站

* [Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/index.html)
* [虚幻在线学习](https://www.unrealengine.com/zh-CN/onlinelearning-courses)
* [An Archive.org backup of wiki.unrealengine.com](https://michaeljcole.github.io/wiki.unrealengine.com/)

#### 书籍

* 《大象无形 - 虚幻引擎程序设计浅析》

#### 视频

* [Unreal Engine C++ Tutorials - YouTube](https://youtube.com/playlist?list=PL3gCaTLUSAUsHG2BzsAs-HIeP08DyWtHh)
* [Learn Unreal Engine (with C++) - YouTube](https://youtu.be/LsNW4FPHuZE)
* [Learn C++ For Unreal Engine - YouTube](https://youtube.com/playlist?list=PLZhNP5qJ2IA0aAwjC3_3kAuF01oG_ol3d)

#### 文章

* [UE4 推荐文章列表 - 知乎专栏](https://zhuanlan.zhihu.com/p/126611976)
* [Unreal Engine 官方程序设计范式分析（Shooter Game） - 看云](https://www.kancloud.cn/ldl19691031/ue-official-programming-pattern/347442)
* [UE 项目的设计规范和代码标准 - 循迹研究室](https://imzlp.com/posts/25915/)

### Blog

* [循迹研究室](https://imzlp.com/)

## 2021-01-27 星期三

### UE4 中的字符串

* [String Handling - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/index.html)
* [Unreal 字符串 FText/FName/FString 浅谈 - cnblog](https://www.cnblogs.com/u3ddjw/p/12307381.html)

### *.generated.h

* [What is *.generated.h header file? - UE4 AnswerHub](https://answers.unrealengine.com/questions/373459/what-is-generatedh-header-file.html#:~:text=MyClass.-,generated.,produce%20code%20in%20the%20generated.)

> *MyClass.generated.h* is the include file generated by the UnrealHeaderTool (before UnrealBuildTool compilation) while parsing unreal macros in *MyClass.h*.
>
> All the **UCLASS, USTRUCT, UPROPERTY, UFUNCTION** macros produce code in the generated.h and so the Blueprint magic can occur in your project with a minimal effort from your side.

### pragma once vs ifndef

* [#pragma once vs ifndef](https://www.avrfreaks.net/forum/pragma-once-vs-ifndef)

> `#pragma once` was originally intended to provide functionality that is a bit different from what include guards do. The idea was that `#pragma once` would permit the preprocessor to cache the names of already-included files. If the same file is included again, the preprocessor would realize it just by looking at the name. It would not even try to locate the file in the file system, let alone re-parse it. This would improve the compiler's performance.

### check() and ensure()

* [When should I use Check? - UE4 AndswerHub](https://answers.unrealengine.com/questions/418935/when-should-i-use-check.html?sort=oldest)

> `check()` is like `assert()` in C. If the condition is false, it will stop your program dead with a log message, an error window and - if a debugger is attached - a break into the debugger. You cannot continue execution after this point.

## 2021-01-25 星期一

### UE4 C++ 编码规范

* [Coding Standard - UE4 Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)

### UE4 工程规范

* [UE5 Style Guide - GitHub](https://github.com/Allar/ue5-style-guide)

### Unity 工程规范

* [Unity Style Guide - GitHub（推荐）](https://github.com/justinwasilenko/Unity-Style-Guide)
* [Unity Style Guide - GitHub](https://github.com/stillwwater/UnityStyleGuide)

### C++ 中 .h 和 .cpp 的作用

* [理解 C++ 中头文件和源文件的作用 - 菜鸟教程](https://www.runoob.com/w3cnote/cpp-header.html)

> .h 文件中能包含：
>
> - 类成员数据的声明，但不能赋值
> - 类静态数据成员的定义和赋值，但不建议，只是个声明就好
> - 类的成员函数的声明
> - 非类成员函数的声明
> - 常数的定义：如：`constint a=5;`
> - 静态函数的定义
> - 类的内联函数的定义
>
> 不能包含：
>
> - 所有非静态变量（不是类的数据成员）的声明
> - 默认命名空间声明不要放在头文件，`using namespace std;` 等应放在 .cpp 中，在 .h 文件中使用 `std::string`

* [What is the difference between #include <filename> and #include "filename"? - stackoverflow](https://stackoverflow.com/questions/21593/what-is-the-difference-between-include-filename-and-include-filename)

> In practice, the difference is in the location where the preprocessor searches for the included file.
>
> For `#include <filename>` the preprocessor searches in an implementation dependent manner, normally in search directories pre-designated by the compiler/IDE. This method is normally used to include standard library header files.
>
> For `#include "filename"` the preprocessor searches first in the same directory as the file containing the directive, and then follows the search path used for the `#include <filename>` form. This method is normally used to include programmer-defined header files.

### UnrealVS 扩展

* [UnrealVS Extension - UE4 Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/UnrealVS/index.html)

### UE4 log 显示优化

* [Change the color of Log Text - Unreal Engine Forums](https://forums.unrealengine.com/development-discussion/c-gameplay-programming/40184-change-the-color-of-log-text)

> I started using cygwin and multitail to achieve colored logs. It takes a bit more doing because you have to regex to get the coloring you want, but you get exactly what you want.
>
> This is the multitail ue4 colorscheme I have so far: (drop this in /etc/multitail.conf)
>
> ```
> colorscheme:ue4
> # Pickout Specials Words etc.
> cs_re:87:LogAbilitySystem
> cs_re:99:Task
> cs_re:99:Ability
> cs_re:9:Fatal
> cs_re:9:Error
> cs_re:3:Warning
> cs_re:11:Display
> cs_re:82:Verbose
> cs_re:81:VeryVerbose
> 
> # General Color Formatting
> cs_re:2:^\[[0-9]*.[0-9]*.[0-9]*-[0-9]*.[0-9]*.[0-9]*:[0-9]*]
> cs_re_s:3:^\[[0-9]*.[0-9]*.[0-9]*-[0-9]*.[0-9]*.[0-9]*:[0-9]*](\[...*\])
> cs_re_s:5:^\[[0-9]*.[0-9]*.[0-9]*-[0-9]*.[0-9]*.[0-9]*:[0-9]*]\[...*\]([^ ]*)
> cs_re_s:6:^\[[0-9]*.[0-9]*.[0-9]*-[0-9]*.[0-9]*.[0-9]*:[0-9]*]\[...*\][^ ]*(.*)
> ```
>
> Also, check out this link for setting up a nice shell (no affiliation with this person, just found it and sharing)
> https://www.trueneutral.eu/2014/win-proper-term.html
>
> **Output of command:**
>
> ```shell
> multitail.exe -cS ue4 <your logfile>.log
> ```
>
> Bonus Links:
>
> \- 256 (Xterm) colors : https://jonasjacek.github.io/colors/
> \- Regex Tester: https://regex101.com/r/nI8xB8/1055

* [Cygwin](https://www.cygwin.com/)
* [MultiTail](https://www.vanheusden.com/multitail/)

## 2021-01-21 星期四

### Gameplay Ability System

* [Gameplay Ability System - UE Documentation](https://docs.unrealengine.com/en-US/InteractiveExperiences/GameplayAbilitySystem/index.html)
* [GAS Documentation - GitHub](https://github.com/tranek/GASDocumentation)
* [UE4 游戏技能系统文档 - CSDN](https://blog.csdn.net/pirate310/article/details/106311256)
* [Gameplay Ability System 插件入门教程 - 博客园](https://www.cnblogs.com/JackSamuel/p/7155500.html)
* [GAS Content - GitHub](https://github.com/Pantong51/GASContent)
* [Gameplay Abilities Slide Show- GoogleDocs](https://docs.google.com/presentation/d/1GeuDO2as1b12ei5OHh6jyfxczVYymXJQDBWoRLDMpOI/edit?usp=sharing)
* [A Guided Tour of Gameplay Abilities | Inside Unreal - YouTube](https://youtu.be/YvXvWa6vbAA)
* [GAS 插件介绍（入门篇）- Bilibili](https://www.bilibili.com/video/BV1X5411V7jh)
* [深入 GAS 架构设计 - Bilibili](https://www.bilibili.com/video/BV1zD4y1X77M)

![image-20210226144235623](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20210226144235623.png)

* [Gameplay Ability System 系统完整学习 - Bilibili](https://www.bilibili.com/video/BV1qh411X7ZN)
* [Introduction to Unreal Engine 4 Ability System - Udemy](https://www.udemy.com/course/introduction-to-unreal-engine-4-ability-system/)
* [Introduction to Unreal Engine 4 Ability System - Bilibili](https://www.bilibili.com/video/BV1NQ4y1K7jR)
* [Gameplay Ability System Tutorial - Youtube](https://youtube.com/playlist?list=PLw-lnbqWlRJCYPwesxD36q8bYq_Yv_mMN)

### PCG 技术

* [近代游戏技术革新与 PCG 技术的思考 - 腾讯 GWB 游戏无界](https://mp.weixin.qq.com/s?__biz=MzA4MDc5OTg5MA==&mid=2650621043&idx=1&sn=5c820d1c916342cba922ce86b6d47f2d&chksm=8797558eb0e0dc9837a8c8986de2e82034f4a2fc2e978042f6bbdacaf2cfdb32e2a1abd61670&mpshare=1&scene=1&srcid=0120SFdvj5guKGDUs4f6yOEB&sharer_sharetime=1611122670451&sharer_shareid=5d7b409587e4faafde1de8c005380dd7&version=3.1.1.3002&platform=win#rd)

### UE 编译游戏项目

* [编译游戏项目 - Unreal Engine](https://docs.unrealengine.com/zh-CN/ProductionPipelines/DevelopmentSetup/CompilingProjects/index.html)

### 编码规范

* [编码规范 - Unreal Engine](https://docs.unrealengine.com/zh-CN/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)

## 2021-01-19 星期二

### UE4 类图

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/image-20210121105932185.png)

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/Ue4_class_tree.png)

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/ue4_class_diagram.png)

### UE4 GamePlay 框架

* [Inside UE4 - 知乎专栏](https://zhuanlan.zhihu.com/p/22813908)
* [GamePlay 架构总结 - 知乎专栏](https://zhuanlan.zhihu.com/p/24170697)

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/v2-b4e0dd15956ccb819fca93e73d1b8ed2_r.jpg)

![](media/PRG-0008-A-Game-Development-Blackboard-Part-3/v2-c0cd2e5121f63c37615f78476e2a425c_r.jpg)

> UGameplayStatics
>
> 我们在蓝图里见到的GetPlayerController、SpawActor和OpenLevel等都是来至于这个类的接口。这个类比较简单，相当于一个C++的静态类，只为蓝图暴露提供了一些静态方法。在想借鉴或者是查询某个功能的实现时，此处往往会是一个入口。

* [GamePlay 架构 Subsystems - 知乎专栏](https://zhuanlan.zhihu.com/p/158717151)

![](media\PRG-0008-A-Game-Development-Blackboard-Part-3\v2-69546312c4c3c05093f94f12b60904cf_r.jpg)

### Multiplayer in Unreal Engine

* [Multiplayer in Unreal Engine: How to Understand Network Replication - YouTube](https://youtu.be/JOJP0CvpB8w)

## 2021-01-12 星期二

### A blank window shows after opening an actor blueprint?

* [A blank window shows after opening an actor blueprint?](https://answers.unrealengine.com/questions/247411/a-blank-window-shows-after-opening-an-actor-bluepr.html)

> If you open a blueprint and the view is mostly blank like above use the menu of that blueprint editor window and click on **Window->Class Defaults**
> This will show you a message at the top that says "Note: This is a data only blueprint, so only the default values are shown. It does not have any script or variables. If you want to add some, Open the Full Blueprint Editor"
> Click the blue link that reads **"Open the Full Blueprint Editor."** You will now be able to use that blueprint again like normal.

### Enable mouse during playing?

* [UE4 Enable Mouse During Playing?](https://stackoverflow.com/questions/43110111/ue4-enabling-mouse-during-play#:~:text=2%20Answers&text=When%20you%20hit%20play%20and,viewport%20by%20pressing%20Shift%2DF1.)

> When you hit play and the game starts, your mouse gets captured by the game to control the camera. If your play button is set to play in the viewport, you can release the mouse from the viewport by pressing **Shift-F1**. The game will still be running, but input (including from the keyboard) will be suspended and you can interact with the editor.

## 2021-01-04 星期一

### Learning Houdini

* [Entagma - YouTube](https://www.youtube.com/channel/UCWu6SQmC6nAZ-reuj3lF2eQ)
* [PDG for Indie Gamedev - SideFX](https://www.sidefx.com/learn/collections/pdg-for-indie-gamedev/)
* [Houdini Engine for Unity - SideFX](https://www.sidefx.com/docs/unity/index.html#Welcome)

-------



​	
