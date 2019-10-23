# Game Development Blackboard - Part 2

## 2019-10-21 星期一

### C# 预编译符号

* 在 Visual Studio `项目 -> 属性 -> 生成 -> 常规`，`条件编译符号`中填入预编译符号，即可让该预编译符号在整个项目中生效。

### 在 Visual Studio 修改项目的程序集名称

* 在 Visual Studio 中，修改了项目名称之后，其相应的程序集名称并没有自动改变，需手动在`项目 -> 属性 -> 应用程序`，修改`程序集名称`和`默认命名空间`。

### .NET 程序集之间相互调用

同一个解决方案下的不同项目之间，或者说不同程序集之间，虽然可以通过引用，让处于依赖层次上层的程序集可以调用到下层的程序集，但由于禁止循环依赖，处于依赖层次下层的程序集，是无法直接调用上层程序集的。

以下两种方法，可以一定程度上实现程序集之间的相互调用。
以上层程序集 A 依赖于下层程序集 B，但下层程序集 B 需要调用上层程序集 A 中的 Model.ClassA 为例：

* 接口与反射

    - 在下层程序集 B 中定义接口 InterfaceB，在上层程序集 A 中，让 Model.ClassA 实现该接口
    - 在下层程序集 B 中，使用反射机制，通过检索程序域中程序集 A，获取 Model.ClassA 对象类型，然后创建该对象实例
    - 在下层程序集 B 中，就可以使用 InterfaceB 引用来持有上层程序集 A 中 Model.ClassA 的对象实例，并通过接口类中定义的接口方法来主动调用对象中的具体实现方法

```csharp
System.Reflection.Assembly[] assemblies = AppDomain.CurrentDomain.GetAssemblies();
foreach (System.Reflection.Assembly assembly in assemblies){    Type type = Type.GetType(Text.Format("{0}, {1}", typeName, assembly.FullName));    if (type != null)    {        return type;    }}
```

* 委托（事件系统）

    - 让上层程序集 A 和下层程序集 B 均引用/依赖于另一个程序集 C，在程序集 C 中实现通用的事件系统并定义事件类型
    - 在上层程序集 A 中订阅/监听事件，该事件是由下层程序集 B 分发/发送的
    - 以此方式即可实现下层程序集 B 调用上层程序集 A 中的具体方法实现

### 动态加载程序集

* [How do I get all assemblies in the solution?](https://www.codeproject.com/Questions/1089179/How-do-I-get-all-assemblies-in-the-solution)
* [Dynamically pre-load assemblies in a ASP.NET Core(or any C#) project](https://dotnetstories.com/blog/Dynamically-pre-load-assemblies-in-a-ASPNET-Core-or-any-C-project-en-7155735300)

```csharp
// Put the right path to the assembly you are trying to load here
string path = @"..\..\ConsoleApplication11\bin\Debug\ConsoleApplication11.exe"; Assembly consoleApp11 = Assembly.LoadFile(path);
```

### 《提问的智慧》

* [How to ask questions the smart way? - GitHub](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way/blob/master/README-zh_CN.md)

## 2019-10-14 星期一

### C# 命名规范

* [Naming Guidelines - Capitalization Styles - Microsoft Docs](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-1.1/x2dbyw72%28v%3dvs.71%29)

**Pascal case (帕斯卡命名法/大驼峰命名法) :**

The first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. You can use Pascal case for identifiers of three or more characters.
For example: `BackColor`.

**Camel case (驼峰命名法/小驼峰命名法) :**

The first letter of an identifier is lowercase and the first letter of each subsequent concatenated word is capitalized.
For example: `backColor`.
 
**Uppercase**

All letters in the identifier are capitalized. Use this convention only for identifiers that consist of two or fewer letters.
For example: `System.IO` and `System.Web.UI`.

## 2019-10-10 星期四

### C# 委托与匿名函数

* [我所理解的委托和匿名函数 - UWA](https://blog.uwa4d.com/archives/2072.html)

> 因为刚才讲到，委托是一种类型，而函数并不是类型，所以通常情况下，如果没有为两种类型提供转型操作，编译器会报出类型不匹配的错误。所以，既然我们这种写法能够通过编译器，那么说明编译器为我们实现了转型操作，比如隐式用于转型的构造函数。（知识点：隐式显示转型构造函数）。
> 如果委托的函数非常简单，或者基本上没有重复利用的可能，那么可以直接把函数体实现写在委托的生成处，这样你就不用费劲心思去思考该怎样给函数取一个容易的名字了，名字压根就不重要了，函数体那几句代码更易于理解代码在干什么，这就是匿名函数，也就是叫做 lambda 表达式的东西。
> 所以要正确使用匿名函数，必须清楚以下几点：>> 1. 尽可能避免匿名函数引用外部变量，让其可被静态化> 2. 搞清楚哪些变量被匿名函数引用了，防止内存泄漏> 3. 尽量把被引用的变量声明放在后面，用变量复制来延迟匿名函数创建

```csharp
// 用ILSpy反编译出来的代码：internal class TestClass {    // 编译器发现这个匿名函数并没有引用外部变量，那么它就可以静态化    // 声明一个静态的委托类型的变量，一次使用的时候初始化    [CompilerGenerated]    private static TestClass.DelegateType <>f__mg$cache0;    public static void Test1() {        int arg_20_0 = 1;        int arg_20_1 = 2;        if ( TestClass.<>f__mg$cache0 == null ) {            // 第一次使用，用函数体构造委托对象，后续使用则不会触发内存分配            TestClass.<>f__mg$cache0 = new TestClass.DelegateType(TestClass.Static_Add);        }        // 看见没，编译器最终传入的是实际生成的委托对象，        // 而不是直接的函数，或者函数指针等等        TestClass.Add( arg_20_0, arg_20_1, TestClass.<>f__mg$cache0 );    }    public static void Test2() {        TestClass @object = new TestClass();        // 委托引用了一个实例对象的成员函数，不能被静态化        // 所以每次调用时，如果不做优化，每次都将产生临时的委托对象        // 如果在程序关键代码中这样写，会导致严重的性能问题        TestClass.Add( 1, 2, new TestClass.DelegateType( @object.Member_Add ) );    }    // 编译为lambda表达式生成了一个对象，用于存储引用的外部变量    // 此方法和我们上文讲的在C++ 中实现一个仿函数的方法完全一样    [CompilerGenerated]    private sealed class <Test3>c__AnonStorey0 {        // Fields        internal TestClass $this;        internal int upvalue;        // Methods        public <Test3>c__AnonStorey0();        internal int <>m__0( int a, int b );    }    public void Test3() {        <Test3>c__AnonStorey0 storey;        // 构造一个临时对象，用于产生委托和存储数据        storey = new <Test3>c__AnonStorey0();        storey.$this = this;        storey.upvalue = 3;        // 该委托引用了非静态数据，所以不能被静态化，需要实时构造        // 这里产生了更多的内存分配操作，使用不当，会引起严重性能问题        Add( 1, 2, new DelegateType( storey.<>m__0 ) );        return;    }}
```

```csharp
// 函数功能：打印从0~9这几个数字// 错误：程序总是输出10，而不是0~9的序列void Error1() {    var printList = new List<Action>();    for ( int i = 0; i < 10; ++i ) {        // 循环里面一直在构造匿名函数对象，分配大量的内存        printList.Add( () => Debug.Log( i ) );    }    for ( int j = 0; j < printList.Count; ++j ) {        printList[ j ](); // 结果总是输出10    }}void Error2() {    var list = new List<int>();    list.Add( 1 );    list.Add( 2 );    int id = 0;    if ( id == 5 ) {
        // 假如满足几率很小        // 表面上看，匿名函数对象在此处构造        // 但实际上，匿名对象在id声明处就已经提前构造好了        // 这样会 100% 造成内存分配        list.Find( value => value == id );    }}

// ====== 反编译后的代码：

void Error1() {    ...    IL_0001: newobj instance void class [mscorlib]System.Collections.Generic.List`1<class [System.Core]System.Action>::.ctor()    ...    IL_002f: ldfld int32 TestClass/'<Error1>c__AnonStorey1'::i    ...    // 说明了匿名函数对象引用的循环变量已经被包裹进了匿名对象内    // 循环变量的值存在堆中，而非栈上了    // 这样导致后面执行函数代码取出来的值都是同一个值}void Error2() {    // 函数体第一个指令就创建了匿名对象    IL_0000: newobj instance void TestClass/'<Error2>c__AnonStorey2'::.ctor()    ...     // id的引用都是匿名对象的成员变量    IL_001d: stfld int32 TestClass/'<Error2>c__AnonStorey2'::id}

// ====== 修正后的正确代码：

void Error1() {    var printList = new List<Action>();    for ( int i = 0; i < 10; ++i ) {        // 为了避免循环变量被引用        // 复制i到局部变量，让其被匿名函数引用        var _i = i;        printList.Add( () => Debug.Log( _i ) );    }    // 结果虽然正确了，但实际编码中，还是要避免循环中构造匿名函数}void Error2() {    var list = new List<int>();    int id = 0;    if ( id == 5 ) {        // 同理，这样匿名函数构造位置延迟到了条件表达式体内        // 消除多数时候的内存分配操作        var _id = id;        list.Find( value => value == _id );    }}
```

* [GCFreeClosure - GitHub](https://github.com/lujian101/GCFreeClosure)

### Unity 编辑器工具制作

* [Unity 手游开发札记（从零开始搭建手游开发的工具集）- 知乎](https://zhuanlan.zhihu.com/p/24557713)
* [Unity 工具类系列教程（配置化和规范教程）- 知乎](https://zhuanlan.zhihu.com/p/30042447)
* [Unity 工具类系列教程（代码自动化生成）- 知乎](https://zhuanlan.zhihu.com/p/30716595)
* [Unity 工具类系列教程（对象池）- 知乎](https://zhuanlan.zhihu.com/p/30575559)

### UGUI 使用

* [UGUI 系列教程（UGUI 基础与界面拼接）- 知乎专栏](https://zhuanlan.zhihu.com/p/28905447)
* [UGUI 系列教程（监听事件，完成解谜）- 知乎专栏](https://zhuanlan.zhihu.com/p/28906086)
* [UGUI 系列教程（OSU 动态界面制作）- 知乎专栏](https://zhuanlan.zhihu.com/p/28906293)
* [UGUI 系列教程（OSU Battle）- 知乎专栏](https://zhuanlan.zhihu.com/p/28906798)

## 2019-10-08 星期二

### Unity I18N

* [Unity I18N 小探 - 知乎](https://zhuanlan.zhihu.com/p/81159633)
* [I2 Localization - Unity Asset Store](https://assetstore.unity.com/packages/tools/localization/i2-localization-14884)

* [游戏国际化的一些建议 - 硬盘在歌唱](http://disksing.com/game-i18n)

> * 不要为每个语言版本建立单独分支
> * 尽量不要针对不同地区写特殊代码
> * 源代码中不能出现汉字或直接用于显示的字符串
> * 服务器代码或配置中不能出现汉字或直接用于显示的字符串
> * 尽量不要使用带文字的图片
> * 设计结构化的字典配置，减少冗余
> * 不用使用 %d、%s 等标识文本中的变量
> * 注意多义词
> * 留意 UI 中文字的长度问题

### Unity 项目资源目录与命名规范

* [Mastering Unity Project Folder Structure. Level 0 - Folders required for version control systems - DEV](http://developers.nravo.com/mastering-unity-project-folder-structure-level-1-reserved-folders/#.XZ3XOI4zYUF)
* [Mastering Unity Project Folder Structure. Level 1 - Reserved Folders - DEV](http://developers.nravo.com/mastering-unity-project-folder-structure-level-1-reserved-folders/#.XZ3XOI4zYUF)
* [Mastering Unity Project Folder Structure. Level 2 - Assets Organization](http://developers.nravo.com/mastering-unity-project-folder-structure-level-2-assets-organization/#.XZ3XQY4zYUE)
* [Best Practices - Folder Structure - Unity Forum](https://forum.unity.com/threads/best-practices-folder-structure.65381/)
* [Unity 工程目录规范 - Moses's Note](https://mrsoong.com/posts/2018-04-01-3743db2c.html)
* [Unity 项目目录结构与命名规则 - 腾讯云](https://cloud.tencent.com/developer/article/1141251)
* [自动化规范 Unity 资源的实践 - UWA](https://edu.uwa4d.com/course-intro/0/121)

### Unity 项目资源制作规范

* [Unity 美术资源制作规范 - Joyimp](http://www.joyimp.com/?post=161)
* [3D 模型与动画，美术资源的规范 - 技术人生](http://www.luzexi.com/2018/08/03/Unity3D%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B%E4%B9%8B%E8%BF%9B%E9%98%B6%E4%B8%BB%E7%A8%8B-3D%E6%A8%A1%E5%9E%8B%E4%B8%8E%E5%8A%A8%E7%94%BB1.html)
* [Unity 美术资源规范整理 - 程序园](http://www.voidcn.com/article/p-qjjvpian-bcw.html)
* [Unity3D 美术资源规范 - 腾讯游戏学院](https://gameinstitute.qq.com/community/detail/128388)
* [美术资源标准（纹理篇） - Unity Connect](https://connect.unity.com/p/mei-zhu-zi-yuan-biao-zhun-wen-li-pian)

### Unity 项目编码规范

* [Unity 之命名规范（一）- 阿里云](https://yq.aliyun.com/articles/666181/)
* [Unity 之命名规范（二）- 阿里云](https://yq.aliyun.com/articles/666180?spm=a2c4e.11153940.0.0.609c684f0u4nXw)

-------


