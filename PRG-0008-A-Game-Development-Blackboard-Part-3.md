# Game Development Blackboard - Part 3

## 2021-01-25 星期一

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

## 2021-01-21 星期四

### Gameplay Abilities System

* [A Guided Tour of Gameplay Abilities | Inside Unreal - YouTube](https://youtu.be/YvXvWa6vbAA)

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




