# Optimization in Unreal Engine

* [Performance and Profiling - UE Documentation](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/PerformanceAndProfiling/)

* [Profiling and Optimization in UE4 | Unreal Indie Dev Days 2019 - YouTube](https://youtu.be/EbXakIuZPFo)

* [UE4 里的性能分析与优化 - 虚幻独立开发日 2019 - bilibili](https://www.bilibili.com/video/av883251191/)

  

* [UE4 项目移动端画面效果适配 - 知乎](https://zhuanlan.zhihu.com/p/145189072)

* [UE4 性能优化指南（程序向）- 知乎](https://zhuanlan.zhihu.com/p/55335907)

* [UE4 性能优化指南（美术向）- 知乎](https://zhuanlan.zhihu.com/p/55335653)

* [UE4 移动平台性能优化：搭建优化流程 - 知乎](https://zhuanlan.zhihu.com/p/97310033)

* [UE4 性能优化方法（工具篇）- 博客园](https://www.cnblogs.com/ghl_carmack/p/5481763.html)

* [UE4 性能优化（个人总结）- 知乎](https://zhuanlan.zhihu.com/p/64187885)

* [UE4 性能分析与优化（方法与工具）- 知乎](https://zhuanlan.zhihu.com/p/213796356)

* [UE4 性能调试分析常用方法 - 知乎](https://zhuanlan.zhihu.com/p/273608458)

# CPU

* [How to improve game thread CPU performance in Unreal Engine? - UE Blog](https://www.unrealengine.com/en-US/blog/how-to-improve-game-thread-cpu-performance)
* [UE4 渲染管线与性能分析系列（CPU 篇）- 知乎](https://zhuanlan.zhihu.com/p/148886428)
* [UE4 的执行流程和 CPU 优化 - 知乎](https://zhuanlan.zhihu.com/p/365764136)

# 内存

# UI

* [UI 性能优化 - 知乎](https://zhuanlan.zhihu.com/p/117577253)

# 包体大小



# 加载

* [PSO Caching - UE Documentation](https://docs.unrealengine.com/4.26/en-US/SharingAndReleasing/PSOCaching/)
* [如何使用 UE4 的 PSO 缓存改善性能 - 知乎](https://zhuanlan.zhihu.com/p/372800310)

# 性能优化实践

## 准备工作

* 关闭垂直同步

```
r.vsync 0
```



* 关闭帧率平滑

```
Project Settings -> Engine -> General Settings -> Smooth Frame Rate
```



## 常用命令

```
stat fps
stat unit
stat game
stat memory
stat screenrendering
stat gpu
stat slow

t.MaxFPS n // 限制最大 FPS（Project Settings 中 Use Fixed Frame Rate 为 false 时，该命令才有效）
r.ScreenPercentage n
sg.PostProcessQuality n // 设置后效质量（0 <= n <= 3）
sg.ShadowQuality n // 设置阴影质量（0 <= n <= 3）
sg.TextureQuality n // 设置纹理质量（0 <= n <= 3）
sg.EffectsQuality n // 设置特效质量（0 <= n <= 3）

stat startfile
stat stopfile
Saved/Profiling/UnrealStats
```



## 性能工具

* Session Frontend

## 减少 Draw Call

* [优化 UE4 性能，减少 Draw Call —— 材质中使用自定义基元数据 - 知乎](https://zhuanlan.zhihu.com/p/215545723)

## 剔除

* 距离剔除
* 视锥体剔除
* 遮挡剔除
* early z pass

## 减少 Over Draw

* Shader Complexity 检查工具

## 材质

## 灯光

* [UE4 Mobile 使用动态阴影的一些小结 - 知乎](https://zhuanlan.zhihu.com/p/90883687)
* Light Complexity 检查工具
* 关闭阴影

## Game Thread

**重点关注**

* FTickFunctionTask：减少需要每帧 Tick 的 Actor 的数量
* BlueprintTime：减少蓝图的消耗
* TickWidgets
* SkinnedMeshCompTick

**常见原因**

* 滥用 Tick
* 引用过多？
* 滥用高消耗的蓝图节点
* 滥用循环

---
change log: 

	- 创建（2021-06-08）

---