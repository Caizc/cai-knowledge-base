# Game Development Blackboard - Part 3

## 2021-12-15 星期三

### Building Unreal Engine from Source

* [Building Unreal Engine from Source - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DevelopmentSetup/BuildingUnrealEngine/)
* [从源码构建虚幻引擎](http://docs.manew.com/ue4/775.html)
* [Versioning of Binaries - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/BuildTools/UnrealBuildTool/VersioningofBinaries/)
* [Compiling Game Projects - UE Documentation](https://docs.unrealengine.com/4.26/en-US/ProductionPipelines/DevelopmentSetup/CompilingProjects/)

### Making an Unreal Engine Installed Build

* [Using an Installed Build - UE Documentation](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DeployingTheEngine/UsinganInstalledBuild/)
* [Unreal Binary Builder - GitHub](https://github.com/ryanjon2040/Unreal-Binary-Builder)

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

### SVN 上传 .so 和 .a 文件

* [SVN 上传不了 .so .a 库可尝试的解决方法 - CSDN](https://blog.csdn.net/brlf_gz/article/details/78402755?spm=1001.2014.3001.5501)

### SVN 递归忽略指定目录

* [Ignore some directories recursively - stackoverflow](https://stackoverflow.com/questions/2035335/svn-ignore-some-directories-recursively)
* [How do I ignore files in SVN? - stackoverflow](https://stackoverflow.com/questions/86049/how-do-i-ignore-files-in-subversion)

> SVN 不区分文件和文件夹，符合规则的文件和目录都会被忽略，但不能对已添加过版本控制的文件进行忽略。

### SVN Cleanup 失败修复方法

* [solution of svn run cleanup failed](https://www.anujvarma.com/svn-cleanup-failedprevious-operation-has-not-finished-run-cleanup-if-it-was-interrupted/)

> 1. Install sqllite
>
> 2. sqlite .svn/wc.db “select * from work_queue”
>
> The SELECT should show you your offending folder/file as part of the work queue. What you need to do is delete this item from the work queue.
>
> 3. sqlite .svn/wc.db “delete from work_queue”

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

### UE4 应用在 Android 平台的启动流程

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

| Unreal Engine Version | Required Android Studio Version | Compatible NDK Versions |
| :-------------------- | :------------------------------ | :---------------------- |
| 4.26.2                | Android Studio 4.0              | NDK r21b                |
| 4.25                  | Android Studio 3.5.3            | NDK r21b, NDK r20b      |
| 4.21 - 4.24           |                                 | NDK r14b                |
| 4.19 - 4.20           |                                 | NDK r12b                |

* [NDK Downloads - Android Developers](https://developer.android.com/ndk/downloads)
* [Packaging Android Projects - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
* [Reducing Packaged Game Size - UE Documentation](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/PerformanceAndProfiling/ReducingPackageSize/)
* [Reducing APK Package Size - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Mobile/Android/ReducingAPKSize/)
* [游戏打包 - 知乎](https://zhuanlan.zhihu.com/p/60996027)

### UE4 iOS Packaging

* [iOS Quick Start - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/QuickStart/)
* [iOS Provisioning - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/iOS/Provisioning/)
* [UE4 打包 iOS 的两种方案 - 知乎](https://zhuanlan.zhihu.com/p/374158520)
* [Apple Developer](https://developer.apple.com/)

### UE4 Patch

* [How to Create a Patch - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/Patching/GeneralPatching/HowToCreatePatch/)

### HotPatcher

* [UE4 Plugin: HotPatcher - GitHub](https://github.com/hxhb/HotPatcher)
* [UE 热更新：需求分析与方案设计 - imzlp.com](https://imzlp.com/posts/17371/)
* [UE 资源热更打包工具 HotPatcher - imzlp.com](https://imzlp.com/posts/17590/)

#### UE4 查看 pak 文件内容

* [UnrealPakViewer - GitHub](https://github.com/jashking/UnrealPakViewer)

## 2021-10-26 星期二

### 引擎中台

* [引擎中台助力《使命召唤手游》技术升级 - 腾讯游戏学堂](https://gameinstitute.qq.com/course/detail/10195)

![img](media/PRG-0008-A-Game-Development-Blackboard-Part-3/QMzhVw3UA9FX1o3ZuG75.jpg)

![img](media/PRG-0008-A-Game-Development-Blackboard-Part-3/Sl1T2Q1wvjfzluEpcIU5.jpg)

## 2021-10-10 星期日

### Support for Google Android App Bundle(AAB) in Unreal Engine 4.24

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
* [啥是 Android App Bundle？- 知乎](https://zhuanlan.zhihu.com/p/61663559)

> * 资源选择性加载
> * 动态下发 lib

* [Packaging Android Projects - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
* [Google Play Asset Delivery Reference - UE Documentation](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/Distribution/GooglePlayAssetDeliveryReference/)
* [Google Play Game's Asset Delivery - YouTube](https://youtu.be/WW9GevpEo1s)
* [Build error: "Installed Build Tools revision 31.0.0 is corrupted" - stackoverflow](https://stackoverflow.com/questions/68387270/android-studio-error-installed-build-tools-revision-31-0-0-is-corrupted)

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

* [Wwise 音频解决方案概述 - 博客园](https://www.cnblogs.com/kekec/p/11714507.html)
* [UE4 中整合 Wwise - 知乎](https://zhuanlan.zhihu.com/p/41761623)
* [Wwise 快速上手指南：程序员篇（v2016.1）- 腾讯游戏学堂](https://gameinstitute.qq.com/community/detail/107700#)
* [示例 - audiokinetic](https://www.audiokinetic.com/zh/library/edge/?source=SDK&id=samplecode.html)
* [SoundBank 的管理策略 - audiokinetic](https://www.audiokinetic.com/zh/library/2019.1.11_7296/?source=Help&id=strategies_for_managing_soundbanks)
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

* [String Handling - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/index.html)
* [Character Encoding - UE4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/CharacterEncoding/index.html)
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

* [UE4 Style Guide - GitHub](https://github.com/Allar/ue4-style-guide)

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

### 代码规范

* [代码规范 - Unreal Engine](https://docs.unrealengine.com/zh-CN/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)

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
