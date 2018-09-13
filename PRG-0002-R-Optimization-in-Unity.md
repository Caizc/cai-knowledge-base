# Optimization in Unity

* [Unity 优化百科 - UWA](https://blog.uwa4d.com/archives/Index.html)

# CPU

* [性能优化，永无止境：CPU篇 - UWA](https://blog.uwa4d.com/archives/optimzation_cpu.html)

CPU 方面的性能开销主要可归结为两大类：**引擎模块**性能开销和**自身代码**性能开销。

## 引擎模块性能优化

### 渲染模块

#### 降低 Draw Call

* 减少所渲染物体的材质种类
* 使用 Draw Call Batching
* Draw Call 并非越低越好，需维持它与总线带宽的平衡

#### 简化资源

* 减少每帧渲染的三角形面片数、网格和纹理资源

#### LOD
#### Occlusion Culling
#### Culling Distance

### UI 模块

#### NGUI

* 最耗时的几个函数：

    - UIPanel.LateUpdate()（CPU 开销最大的函数）
    - UICamera.Update()
    - UIRect.Update()
    - UIRect.Start()

* 对于 **UIPanel.LateUpdate()** 的优化，主要着眼于 UIPanel 的布局，其原则如下：

    - 尽可能将动态 UI 元素和静态 UI 元素分离到不同的 UIPanel 中（ UI 的重建以 UIPanel 为单位），从而尽可能将因为变动的 UI 元素引起的重构控制在较小的范围内
    - 尽可能让动态 UI 元素按照同步性进行划分，即运动频率不同的 UI 元素尽可能分离放在不同的 UIPanel 中
    - 控制同一个 UIPanel 中动态 UI 元素的数量，数量越多，所创建的 Mesh 越大，从而使得重构的开销显著增加。比如，战斗过程中的 HUD 运动血条可能会出现较多，此时，建议研发团队将运动血条分离成不同的 UIPanel，每组 UIPanel 下 5~10 个动态 UI 为宜。这种做法，其本质是从概率上尽可能降低单帧中 UIPanel 的重建开销

#### UGUI

### 加载模块

加载模块的性能开销主要集中在**场景切换**时，且 CPU 占用峰值较高，主要包括了**上一场景的卸载**和**下一场景的加载**两个方面。

#### 场景卸载

场景卸载一般由引擎自动完成，即当我们调用类似 Application.LoadLevel 的 API 时，引擎会开始对上一场景进行处理，其性能开销主要分为以下几个部分：

* **Destroy**
    引擎在切换场景时会收集所有未标识为 `DontDestoryOnLoad` 的 GameObject 及其 Component ，然后进行 Destroy。同时，代码中的 `OnDestory()` 被触发执行，这里的性能开销主要取决于 `OnDestroy()` 回调函数中的代码逻辑。

* **Resources.UnloadUnusedAssets**
    一般情况下，场景切换过程中，该 API 会被调用两次，一次为引擎在切换场景时自动调用，另一次则为用户手动调用（一般出现在场景加载后，用户调用它来确保上一场景的资源被卸载干净）。该 API 的 CPU 开销主要集中在 500ms~3000ms 之间。其耗时开销**主要取决于场景中 Asset 和 Object 的数量**，数量越多，则耗时越多。

#### 场景加载

* **资源加载**
    资源加载几乎占据整个加载过程的 90% 以上时间，其加载效率主要取决于：

    - 资源的加载方式（Resource.Load 或 AssetBundle 加载）
    - 加载量（纹理、网格、材质等资源数据的大小）
    - 资源格式（纹理格式、音频格式等）

    不同的加载方式、不同的资源格式，其加载效率有很大差别。

* **Instantiate 实例化**

    - 实例化操作时，引擎底层会查看相关资源是否已经被加载，如果没有，则会先加载相关的资源，再进行实例化。所以应该**根据 AssetBundle 资源依赖关系打包并进行预加载**，以缓解 Instantiate 实例化时的压力
    - 脚本代码中**序列化**操作过多也会导致 Instantiate 实例化时间变长。

### 动画系统

### 物理系统

### 粒子系统

### GC 调用

## 代码模块性能优化

绝大多数项目中的性能开销都遵循「二八原则」，即 80% 的性能开销都集中在 20% 的函数上。

# 内存

* [性能优化，进无止境：内存篇（上）- UWA](https://blog.uwa4d.com/archives/optimzation_memory_1.html)
* [性能优化，进无止境：内存篇（下）- UWA](https://blog.uwa4d.com/archives/optimzation_memory_2.html)
* [关于 Unity 内存优化，你可能遇到这些问题 - UWA](https://blog.uwa4d.com/archives/QA_Memory-1.html)

## 内存泄露

* [深入浅出再谈 Unity 内存泄漏 - WeTest](https://wetest.qq.com/lab/view/150.html)
* [扒一扒 Profiler 中这几个“占坑鬼” - UWA](https://blog.uwa4d.com/archives/presentandsync.html)

## 内存泄露排查工具

* [Unity MemoryProfiler - bitbucket](https://bitbucket.org/Unity-Technologies/memoryprofiler)
* [Unity 5.3 新 Memory Profiler - 简书](https://www.jianshu.com/p/171d63ed8ba0)
* [使用 Unity 新的 Memory Profiler - 简书](https://www.jianshu.com/p/b6562986fc99)

* [DetectLeaks - wiki Unity 3D](https://wiki.unity3d.com/index.php?title=DetectLeaks)

* [Unity 内存泄露之 Render 的 sharedMaterial 和 material - 程序园](http://www.voidcn.com/article/p-mnynllwh-bee.html)
* [Unity 内存优化教程笔记 - CSDN](https://blog.csdn.net/wwanrong/article/details/78676275)

* [Unity Memory Porfiler 的工作机制及可能的改进 - 顾路的博客](http://gulu-dev.com/post/perf_assist/2017-01-25-unity-memoryprofiler)
* [PerfAssist - GitHub](https://github.com/GameBuildingBlocks/PerfAssist/)

# GPU

---

change log: 

	- 创建（2017-12-19）
	- 增加内存优化相关内容（2018-09-07）

---

