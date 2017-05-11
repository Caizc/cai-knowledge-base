# Roberto Ierusalimschy-《Programming in Lua》

* **Programming in Lua**
* 《Lua 程序设计（第 2 版）》
* [巴西] `Roberto Ierusalimschy` 著
* 2008 年 5 月

![](media/14934801635148.jpg)

-------

**第一部分**

# 开始

```lua
print("Hello World!")
```


```lua
function pairsByKeys (t, f)
    local a = {}
    for n in pairs(t) do
        a[#a + 1] = n
    end

    table.sort(a, f)

    local i = 0

    return function ()
        i = i + 1
        return a[i], t[a[i]]
    end
end

local lines = { boy = 2, apple = 1, dog = 4, cat = 3}

local function sortfunction (a, b)
    return a > b
end

for name, line in pairsByKeys(lines, sortfunction) do
    print(name, line)
end
```

## chunk（程序块）



## 词法规范
## global variables（全局变量）
## interperter（解释器程序）

# 类型与值

* nil
* boolean
* number
* string
* table
* function
* userdata
* thread

# 表达式

* 算术操作符
* 关系操作符
* 逻辑操作符
* 字符串连接
* 优先级
* table constructor（table 构造式）

# 语句

* 赋值
* local variables & block（局部变量与块）
* 控制结构

    - if then else
    - while
    - repeat
    - numeric for（数字型 for）
    - generic for（泛型 for）

* break & return

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

[Lua简明教程 | | 酷 壳 - CoolShell](http://coolshell.cn/articles/10739.html)

---

change log: 

	- 创建（2017-04-29）
	- 更新（2017-05-10）

---

