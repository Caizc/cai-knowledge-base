# Game Design Blackboard

## 2020-03-05 星期四

### 圆桌理论

* [圆桌理论 - 百度百科](https://baike.baidu.com/item/%E5%9C%86%E6%A1%8C%E7%90%86%E8%AE%BA/6817139?fr=aladdin)

## 2019-09-11 星期三

### 开放世界

* [当我们说开放世界的时候，我们到底是在说些什么？- IndieNova](https://indienova.com/indie-game-development/what-we-talking-about-open-world-when-talking-about-it/)

## 2019-08-01 星期四

### 技能系统设计

* [可扩展技能系统 - Photone Ray](http://www.photoneray.com/ability-system/)
> 如果一个技能在正确的时间点，播放了合适的技能效果，造成了准确的反馈，那可以说，这个技能表现是对的。
> 对于如今技能表现基本靠模型动作和技能特效的游戏来说，如果模型动作与技能特效出现的时间点和位置符合心里预期的话，那这个技能表现就具备一定的真实性，俗称打击感。
> 技能施放的正确与否，关注技能的出手点与反馈点，前者由设计人员配置，后者由程序生成（如碰撞检测到）。
> 技能的可扩展性表现在配置、执行脚本、程序接口三者分离。
> 配置提供技能对象的属性，脚本提供技能对象的方法，而程序就是加载配置与脚本生成技能对象，并让技能对象运作起来。（这三者不只适用于描述技能系统）
> 技能不是buff，只是产生buff

* [战斗中的取消：《战神》与动作游戏设计 - 程序园](http://www.voidcn.com/article/p-arhkycqd-xq.html)
* [从《暗黑 3》开始：动作游戏战斗系统浅析 - 程序园](http://www.voidcn.com/article/p-cjnnfmsm-bno.html)

## 2019-05-05 星期日

### 三消游戏

* [三消游戏发展史 - 知乎专栏](https://zhuanlan.zhihu.com/p/27864676)
* [三消游戏的难度探讨 - 知乎专栏](https://zhuanlan.zhihu.com/p/28018187)
* [三消游戏元素与关卡设计 - 知乎专栏](https://zhuanlan.zhihu.com/p/28094734)
* [如何做三消游戏的策略性研究？以 Candy Crush 为例 - 腾讯游戏学院](https://gameinstitute.qq.com/community/detail/110566)
* [《英雄纹章》（Hero Emblems）：战斗消除的新标杆 - 触乐](http://www.chuapp.com/2015/01/30/122365.html)
* [Hero Emblems 全攻略](https://forum.gamer.com.tw/C.php?bsn=27690&snA=38&tnum=4)

## 2018-09-10 星期一

### 游戏关卡设计

[多人游戏关卡设计视觉化指南](http://kirozhang1997.com/2018/01/26/GameDesignGuideTrans/)

## 2018-03-07 星期三

### 技能系统设计

* [从技能设计复杂度及定位谈被动技能 - GameRes](http://bbs.gameres.com/thread_328718_1_1.html)

* [如何设计一个易扩展的游戏技能系统？- 知乎](https://www.zhihu.com/question/29545727)

**技能系统核心功能有两个，一个是定义表现流程，一个是处理逻辑效果。**
所谓表现流程就是角色在什么时候播放什么动画、特效、音效，什么时候判定伤害，什么时候发射抛射物。
所谓逻辑效果就是技能给目标造成多少伤害，附加什么buff/debuff效果。在我设计的技能系统中，核心基础是lua脚本，通过lua脚本处理复杂的技能逻辑。

基础内容有这么几个部分：

* **Actor**，这个是角色本身，它不属于技能系统，但是它要给技能系统开放足够的接口，比如播放动画、播放声音、控制位移、造成伤害、添加buff等等
* **Skill**，这个就是技能本身，它在合适的时机调用脚本中的相应函数，脚本中可以在OnCreate  OnHit  OnDeath  OnHeroDeath  OnSoldierDeath等事件中写相应代码。由于是脚本，所以代码非常灵活，而由于限定了只处理技能相关功能，所以代码也不会很复杂，有经验的策划绝对搞的定。
* **Buff**，这个是技能效果的核心。它可以是有时限的，也可以是被动无时限的。在它对应的脚本中，定义了这个Buff会影响哪些角色属性（如血量、暴击、攻击力等等）或者角色状态（如眩晕、隐身、沉默等等），同样，buff脚本也支持事件机制，在脚本的相应事件处理其逻辑功能，可以实现非常丰富的效果。
* **Modifier**，这个是一个技能修改器。技能修改器可以修改技能的流程和效果（比如技能伤害增加、火球击中人会爆炸等等），具体可以参考风暴英雄中的技能天赋系统。技能修改器并没有脚本与之对应，一个技能如果支持某个修改器，需要在脚本中处理相应功能。

* [Buff 机制及其实际运用 - GameRes](http://bbs.gameres.com/forum.php?mod=viewthread&tid=215027)

Buff 是一种回调机制，在必要的时候进行逻辑回调。
Buff 回调点：

1. BuffOccur
2. BuffOnTick
3. BuffRemoved
4. BuffBeHurt
5. BuffOnHit
6. BuffBeforeKilled
7. BuffAfterKilled

* [通用型buff机制在实战中的运用 - GameRes](http://bbs.gameres.com/thread_454153.html)

1、Buff 在同一款游戏中并非只能有一套
2、Buff 机制并非只能在 ARPG 中使用
3、现实生活中也有 Buff 机制的落脚点

* [游戏 BUFF 设计 - cnblogs](http://www.cnblogs.com/damowang/p/5799967.html)

总体上来说，BUFF/DEBUFF都属于“临时的技能效果”，因此它们可以沿用绝大部分的技能逻辑对角色进行程序处理。

设计一个BUFF/DEBUFF机制，需要考虑这么几个要点：

内部运算：
1、是否包含技能效果？（提高/降低 攻击 命中 闪避 移动速度  群体伤害 替换技能ID 等 ）
2、是否包含阶段效果？（BUFF分为多个阶段，不同的阶段有不同的效果，比如影之哀伤）
3、是否包含计时器？（持续时长计算、叠加时长计算 总之所有关于持续性时间的问题 都丢这里）
4、是否包含计数器？（用来计算阶段、剩余生效次数、比如影之哀伤 LOL电刀）
5、是否具备分类规则？（魔法效果 诅咒效果 中毒效果 用于进行归类 方便程序进行的 驱散筛选判断）
6、是否可以被驱散？ （魔法效果只能用祛除魔法解除 中毒效果只能用解药祛除）
7、是否具备优先级？（附加优先级，低等级BUFF会被高等级BUFF替换，低等级BUFF无法附加给高等级怪）
8、是否保留母体信息？（比如传染性的DEBUFF，感染者传播一次，母体会获得额外巴拉巴拉。。。多个项）
9、是否共享同步规则？（比如多个角色共享一个BUFF状态，一个人的BUFF被祛除则其他人也被祛除）
10、以上功能可以进行再补充，没有需求则可以逐个剔除。

外部表现：
1、是否显示BUFF图标？（传奇里道士的BUFF是不显示图标的）
2、是否不同阶段表现不同的图标？
3、是否显示计时器？
4、是否显示计数器？
5、是否显示BUFF文字说明？（对BUFF类型、效果的描述）
6、是否改变角色外形？（DNF里的冰冻、WOW里的变形）
7、以上表现功能可以进行再补充，同上。

* [策划公式的 DSL 设计 - 云风的 BLOG](https://blog.codingnow.com/2012/01/dev_note_8.html)
* [AOE机制的DSL及其实际运用 - GameRes](http://bbs.gameres.com/forum.php?mod=viewthread&tid=225054)

* [不要用海量表项压垮“技能流程” - GameRes](http://bbs.gameres.com/thread_229210_1_1.html)

技能，说穿了只是一个流程，而不该是一个实体。

* [手游回合制游戏战斗机制归纳式设计 - GameRes](https://bbs.gameres.com/forum.php?mod=viewthread&tid=259895)

* [游戏开发笔记（九）——技能系统 - CSDN](http://blog.csdn.net/mooke/article/details/9771545)

对于技能系统这个比较大的主题，通常要先拆小了来分析。也许不太恰当，但姑且先分为动作表现、技能逻辑和伤害判定这三块吧。

## Overwatch

* [《守望先锋》PVP系统分析：核心玩法、数值平衡与奖励机制](http://www.gameres.com/666145.html)

## 英雄无敌

《英雄无敌：战争纪元》卡牌游戏

* [英雄无敌-战争纪元 简析 - GAD](http://gad.qq.com/article/detail/38169#)
* [《英雄无敌-战争纪元》简析](http://bbs.gameres.com/thread_788641_1_1.html)

-------


