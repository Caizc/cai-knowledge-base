# Roberto Ierusalimschy-《Programming in Lua》

* **Programming in Lua**
* 《Lua 程序设计（第 2 版）》
* [巴西] `Roberto Ierusalimschy` 著
* 2008 年 5 月

![](media/14934801635148.jpg)

-------

**第一部分**

# 起点

在 `hello.lua` 文件中编写代码：

```lua
print("Hello World!")
```

在命令行中运行：

`$ lua hello.lua`

## Chunk（程序块）

* 在交互模式中运行 Lua 解析器
* 使用 `dofile` 函数连接外部 chunk，`dofile` 函数加载文件并执行它

## 词法约定

* 标识符
* 字母的含义依赖于本地环境 Locale（区域设置）
* 保留字

```lua
and        break      do         else       elseif
end        false      for        function   if
in         local      nil        not        or
repeat     return     then       true       until
while
```

* 大小写敏感
* 单行注释 --
* 多行注释 --[[ --]]

```lua
--[[
print(10)         -- no action (comment)
--]]
```

## global variables（全局变量）

* 全局变量不需要声明，给一个变量赋值后即创建了这个全局变量
* 访问一个没有初始化的全局变量不会出错，只不过得到的结果是 nil
* 将一个全局变量赋值为 nil 即可删除它
* 当且仅当一个变量不等于 nil 时，这个变量才存在

## 命令行方式

`lua [options] [script [args]]`

-e：直接将命令传入 Lua
-l：加载一个文件
-i：进入交互模式

* `_PROMPT` 内置变量作为交互模式的提示符：

```
$ lua -i -e "_PROMPT=' lua> '"
lua>
```

* 环境变量 `LUA_INIT`

-------

# 类型与值

* 函数 `type` 可以测试给定变量或值的类型

```lua
print(type("Hello world"))      --> string
print(type(10.4*3))             --> number
print(type(print))              --> function
print(type(type))               --> function
print(type(true))               --> boolean
print(type(nil))                --> nil
print(type(type(X)))            --> string
```

* 变量没有预定义的类型，每一个变量都可能包含任一种类型的值
* 一般情况下同一变量代表不同类型的值会造成混乱，最好不要用，但是特殊情况下可以带来便利，比如使用 `nil` 来表示异常情况

## nil

* Lua 中的特殊类型，只有一个值 `nil`，主要功能是用于区别其他任何值

## boolean

* 有两个取值：`false` 和 `true`
* Lua 中所有的值都可以作为条件
* Lua 将 `false` 和 `nil` 视为「假」，其他值都为「真」
* Lua 认为`数字 0` 和`空字符串`都是「真」

## number

* number 类型用于表示实数，Lua中没有整数

## string

* Lua 中字符串是不可以修改的
* 可以使用单引号或者双引号表示字符串
* 转义符 `\`
* 使用 `[[...]]` 表示字符串
* Lua 会自动在 string 和 number 之间自动进行类型转换
* 字符串连字符 `..`
* 当在一个数字后面写 `..` 时，必须加上空格以防止被解释错
* 使用函数 `tonumber` 显式的将 string 转为 number
* 使用函数 `tostring` 显式的将 number 转为 string

## table
## function

* 函数是第一类值（和其他变量相同），可以存储在变量中，可以作为函数的参数，也可以作为函数的返回值
* Lua 可以调用 lua 或者 C 实现的函数，Lua 所有标准库都是用 C 实现的

## userdata & thread

* userdata 可以将 C 数据存放在 Lua 变量中，userdata 在 Lua 中除了赋值和相等比较外没有预定义的操作
* userdata 用来描述应用程序或者使用 C 实现的库创建的新类型

-------

# 表达式

* Lua 中的表达式包括数字常量、字符串常量、变量、一元和二元运算符、函数调用
* 还可以是非传统的函数定义和表构造

## 算术运算符

* 二元运算符：`+ - * / ^`（加减乘除幂）
* 一元运算符：`-`（负值）
* 这些运算符的操作数都是实数

## 关系运算符

```lua
<      >      <=     >=     ==     ~=
```

* 关系操作符返回结果为 `false` 或 `true`
* `==` 和 `~=` 比较两个值，如果两个值类型不同，Lua 认为两者不同
* `nil` 只和自己相等
* Lua 通过引用比较 table、userdata、function，也就是说当且仅当两者表示同一个对象时相等
* Lua 比较数字按传统的数字大小进行，比较字符串按字母的顺序进行，但是字母顺序依赖于本地环境
* 为了避免不一致的结果，混合比较数字和字符串，Lua 会报错，比如：`2 < "15"`

## 逻辑运算符

```lua
and    or     not
```

* 逻辑运算符认为 `false` 和 `nil` 是 `false`，其他为 `true`，`0` 和 `""` 也是 `true`
* `and` 和 `or` 的运算结果不是 `true` 和 `false`，而是和它的两个操作数相关：

```lua
a and b       -- 如果a为false，则返回a，否则返回b
a or  b        -- 如果a为true，则返回a，否则返回b
```

* 实用技巧：如果 `x` 为 `false` 或者 `nil` 则给 `x` 赋初始值 `v`：

```lua
x = x or v
```
等价于：
```lua
if not x then
    x = v
end
```

* `and` 的优先级比 `or` 高
* C 语言中的三元运算符 `a ? b : c`，在 Lua 中可以这样实现：`(a and b) or c`
* `not` 的结果只返回 `false` 或者 `true`

## 连接运算符

```lua
..         --两个点
```

* 如果操作数为数字，Lua将数字转成字符串

## 优先级

* 从高到低的顺序：

```lua
^
not    - (unary)
*      /
+      -
..
<      >      <=     >=     ~=     ==
and
or
```

* 除了 `^` 和 `..` 外所有的二元运算符都是左连接的

## 表的构造

* 最简单的构造函数是 `{}`，用来创建一个空表
* 数组的第一个元素是索引为 `1`，而不是通常的 `0`
* 构造函数可以使用任何表达式初始化
* list 风格的构造函数：

```lua
days = {"Sunday", "Monday", "Tuesday", "Wednesday",
              "Thursday", "Friday", "Saturday"}
```

* record 风格的构造函数：

```lua
a = {x=0, y=0}       --等价于       a = {}; a.x=0; a.y=0
```

* 在同一个构造函数中可以混合 list 风格和 record 风格进行初始化：

```lua
polyline = {color="blue", thickness=2, npoints=4,
              {x=0,   y=0},
              {x=-10, y=0},
              {x=-10, y=1},
              {x=0,   y=1}
}
```

* 可以嵌套构造函数来表示复杂的数据结构
* 不管用何种方式创建 table ，我们都可以向表中添加或者删除任何类型的域，构造函数仅仅影响表的初始化
* 更一般的初始化方式，可以用 `[expression]` 显示的表示将被初始化的索引：

```lua
opnames = {["+"] = "add", ["-"] = "sub",
              ["*"] = "mul", ["/"] = "div"}
 
i = 20; s = "-"
a = {[i+0] = s, [i+1] = s..s, [i+2] = s..s..s}
 
print(opnames[s])    --> sub
print(a[22])         --> ---
```

list 风格初始化和 record 风格初始化是这种一般初始化的特例：

```lua
{x=0, y=0}        --等价于       {["x"]=0, ["y"]=0}
{"red", "green", "blue"}        --等价于  {[1]="red", [2]="green", [3]="blue"}
```

* 不推荐数组下标从 `0` 开始，否则很多标准库不能使用
* 通常使用分号用来分割不同类型的表元素：

```lua
{x=10, y=45; "one", "two", "three"}
```

-------

# 语句

## 赋值语句

* 多个变量同时赋值：

```lua
a, b = 10, 2*x       --等价于       a=10; b=2*x
```

* 遇到赋值语句 Lua 会先计算右边所有的值然后再执行赋值操作，所以可以这样进行交换变量的值：

```lua
x, y = y, x                     -- swap 'x' for 'y'
a[i], a[j] = a[j], a[i]         -- swap 'a[i]' for 'a[i]'
```

* 当变量个数和值的个数不一致时，Lua 会一直以变量个数为基础采取以下策略：

```lua
变量个数 > 值的个数             按变量个数补足nil
变量个数 < 值的个数             多余的值会被忽略
```

* 多值赋值经常用来交换变量，或将函数调用返回给变量：

```lua
a, b = f()          --      f()返回两个值，第一个赋给a，第二个赋给b
```

## 局部变量与代码块

* 使用 local 创建一个局部变量，与全局变量不同，局部变量只在被声明的那个代码块内有效
* 代码块：指一个控制结构内，一个函数体，或者一个 chunk（变量被声明的那个文件或者文本串）
* `do..end` 块（相当于 c/c++ 的 `{}`）
* 应该尽可能的使用局部变量，有两个好处：

    - 避免命名冲突
    - 访问局部变量的速度比全局变量更快

* 给 block 划定一个明确的界限：`do..end` 内的部分，当你想更好的控制局部变量的作用范围的时候很有用

```lua
do
    local a2 = 2*a
    local d = sqrt(b^2 - 4*a*c)
    x1 = (-b + d)/a2
    x2 = (-b - d)/a2
end            -- scope of 'a2' and 'd' ends here
 
print(x1, x2)
```

## 控制结构语句

* `if` 语句的三种形式：

```lua
if conditions then
    then-part
end;
 --
if conditions then
    then-part
else
    else-part
end;
 --
if conditions then
    then-part
elseif conditions then
    elseif-part
..            --->多个elseif
else
    else-part
end;
```

* `while` 语句

```lua
while condition do
    statements;
end;
```

* `repeat-until` 语句

```lua
repeat
    statements;
until conditions;
```

* **numeric for**（数值 for 循环）
* **generic for**（泛型 for）

## break & return

# 函数

* multiple results（多重返回值）
* variable number of arguments（变长参数）
* named arguments（具名实参）

# 深入函数

* closure（闭合函数）
* non-global function（非全局函数）
* proper tail call（正确的尾调用）

# 迭代器与泛型 for

* iterator & closure
* 泛型 for 的语义
* 无状态的迭代器
* 具有复杂状态的迭代器
* 真正的迭代器

# 编译、执行与错误

* 编译
* C 代码
* error（错误）
* 错误处理与异常
* 错误消息与 traceback（追溯）

# coroutine（协同程序）

* 协同程序基础
* pipe（管道）与 filter（过滤器）
* 以协同程序实现迭代器
* non-preemptive（非抢先式）的多线程

# 完整的示例

* 数据描述
* markov chain 算法

-------

**第二部分**

# 数据结构

* 数组
* 矩阵和多维数组
* 链表
* 队列与双向队列
* 集合与无序组（bag）
* 字符串缓冲
* 图

# 数据文件与持久性

* 数据文件
* Serialization（串行化）

    - 保存无环的 table
    - 保存有环的 table

# metatable（元表）与 metamethod（元方法）

* 算术类的元方法
* 关系类的元方法
* 库定义的元方法
* table 访问的元方法

    - __index 元方法
    - __newindex 元方法
    - 具有默认值的 table
    - 跟踪 table 的访问
    - 只读的 table

# 环境

* 具有动态名字的全局变量
* 全局变量声明
* 非全局的环境

# 模块与包

* require 函数
* 编写模块的基本方法
* 使用环境
* module 函数
* 子模块与包

# 面向对象编程

* 类
* 继承
* 多重继承
* 私密性
* single-method（单一方法）

# 弱引用 table

* memorize（备忘录）函数
* 对象属性
* table 的默认值

-------

**第三部分**

# 数学库

# table 库

* 插入与删除
* 排序
* 连接

# 字符串库

* 基础字符串函数
* pattern-matching（模式匹配）函数

    - string.find
    - string.match
    - string.gsub
    - string.gmatch
   
* 模式
* capture（捕获）
* 替换

    - URL 编码
    - tab 扩展

* 技巧 

# I/O 库

* 简单 I/O 模型
* 完整 I/O 模型

    - 性能小诀窍
    - 二进制文件
    - 其他文件操作

# 操作系统库

* 日期和时间
* 其他系统调用

# 调试库

* 自省机制

    - 访问局部变量
    - 访问 non-local variable（非局部变量）
    - 访问其他协同程序

* hook
* profile（性能剖析）

-------

**第四部分**

# C API 概述
# 扩展应用程序
# 从 Lua 调用 C
# 编写 C 函数的技术
# 用户自定义类型
# 管理资源
# 线程和状态
# 内存管理


-------

# 延伸阅读

[Lua 程序设计 - 中国 Lua 开发者](http://www.shouce.ren/api/lua/5/_3.htm)
[Lua 教程 - RUNOOB.COM](http://www.runoob.com/lua/lua-tutorial.html)
[Lua简明教程 | | 酷 壳 - CoolShell](http://coolshell.cn/articles/10739.html)
[Lua Unofficial FAQ](http://www.luafaq.org/)
[Lua 5.1 参考手册 - 云风译](http://www.codingnow.com/2000/download/lua_manual.html)

---

change log: 

	- 创建（2017-04-29）
	- 更新（2017-05-10）

---

