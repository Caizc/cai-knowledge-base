# Scripting - Unity Manual

![](media/15022679545708.jpg)

[Scripting - Unity Manual](https://docs.unity3d.com/Manual/ScriptingSection.html)

# Scripting - Tutorials

[Scripting - Unity Learn](https://unity3d.com/learn/tutorials/s/scripting)

## Beginner Gameplay Scripting

### Awake & Start

* **Awake** 方法在脚本组件为 `disabled` 的时候依然会被调用，而 **Start** 方法只有在脚本组件为 `enabled` 的时候才会被调用，且在其生命周期中仅被调用一次。

### Update & FixedUpdate

### Vector Maths

* `Vector3.magnitude`
    向量的模，即向量的长度。

* `Vector3.Dot(Vector3 lhs, Vector3 rhs)`
    两个向量的点乘。当两个向量的点乘为 0 时，它们互相垂直；大于 0 时，它们朝向相同；小于 0 时，它们朝向相反。

* `Vector3.Cross(Vector3 lhs, Vector3 rhs)`
    两个向量的叉乘。两个向量的叉乘为同时垂直于这两个向量的一个新向量，新向量的方向取决于坐标系的类型（「左手坐标系」还是「右手坐标系」）。

### Enabling and Disabling Components

* `Behaviour.enabled`

### Activating GameObjects

* `GameObject.SetActive(bool value)`
    激活或者关闭一个 GameObject。当父 GameObject 为关闭的时候，其下的子 GameObject 也均关闭，此时无法通过设置子 GameObject 的 `SetActive` 方法来激活子 GameObject。

* `GameObject.activeSelf`
    返回该 GameObject 自身的激活状态。

* `GameObject.activeInHierarchy`
    返回该 GameObject 在场景中是否激活。仅当该 GameObject 本身及其所有父 GameObject 均为激活时，该属性才为 `true`。

### Translate and Rotate

* `Transform.Translate(Vector3 translation, Space relativeTo = Space.Self)` & `Transform.Rotate(Vector3 eulerAngles, Space relativeTo = Space.Self)`
    `Translate` 和 `Rotate` 方法分别用于**非刚体对象**（non-rigidbody object）的位置移动和方向转动。

### Look At

* `Transform.LookAt(Transform target)`
    将该对象的 z 轴始终指向目标对象，该方法经常应用于摄像头上，以持续追踪某个对象。

### Linear Interpolation

* `Mathf.SmoothDamp(float current, float target, ref float currentVelocity, float smoothTime, float maxSpeed = Mathf.Infinity, float deltaTime = Time.deltaTime)`
    随着时间平滑地将值 `current` 过渡到值 `target`，该方法可以用于平滑任意类型的值、位置、颜色或者缩放等。
    一般情况下，**应优先使用 SmoothDamp 方法来实现平滑过渡效果**，而不是使用 Lerp 进行线性插值，除非你想得到特定的效果。

* `Mathf.Lerp(float a, float b, float t)`
    使用百分比 `t` 对 `a` 值到 `b` 值之间线性插值，`t` 的值为 `[0,1]`。当 `t` 为 `0` 时，返回 `a` 值；当 `t` 为 `1` 时，返回 `b` 值。

* `Color.Lerp(Color a, Color b, float t)`
    使用百分比 `t` 对颜色 `a` 到颜色 `b` 之间线性插值。

* `Vector3.Lerp(Vector3 a, Vector3 b, float t)`
    使用百分比 `t` 对向量 `a` 到向量 `b` 之间线性插值。

### Destroy

* `Object.Destroy(Object obj, float t = 0.0F)`
    用于移除 GameObject、Component 或 Asset，第二个参数 `t` 为可选的销毁延时时间。
    **实际上的对象销毁操作会被推迟到 Update 循环之后、渲染之前执行。**

### GetButton and GetKey

* `Input.GetKey(string name)`
    返回相应的**键盘按键**是否被按下。
    建议在处理输入时使用 `Input.GetAxis` 和 `Input.GetButton` 作为替代，因为这两个方法允许终端用户对按键映射进行配置。

* `Input.GetButton(string buttonName)`
    返回相应的**虚拟按钮**是否被按下，`buttonName` 对应的实际按键在 InputManager 中设置。
    一般使用该方法来触发一个动作，比如开枪，而一般使用 `GetAxis` 方法来获取控制持续移动的输入。

* `Input.GetButtonDown(string buttonName)` & `Input.GetButtonUp(string buttonName)`
    仅当用户按下或抬起指定的虚拟按钮的**那一帧**返回 `ture`。

* [按键标识列表 - Unity Manual](https://docs.unity3d.com/Manual/ConventionalGameInput.html)
* [InputManager - Unity Manual](https://docs.unity3d.com/Manual/class-InputManager.html)

### GetAxis

* `Input.GetAxis(string axisName)`
    返回指定虚拟轴的平滑过渡值，该 float 值为 `[-1,1]` 之间。

* `Input.GetAxisRaw(string axisName)`
    返回指定虚拟轴的原始值，该 float 值始终为 `-1, 0, 1` 中的一个。

### OnMouseDown

* `MonoBehaviour.OnMouseDown()`
    当在一个 **GUI 元素**或者 **Collider** 上按下鼠标时，这个方法会被调用。
    这个方法的调用**依赖于射线检测**。

### GetComponent

* `Component.GetComponent(Type type)`
    获得附加在 GameObject 上的指定 Component 的引用。
    **GetComponent 方法的执行需要耗费一定的处理器性能，应该尽可能少的调用它，仅在 Awake、Start 或者首次使用它的时候调用。** 

### Delta Time

* `Time.deltaTime`
    完成上一帧所耗费的秒数（只读）。
    **使用该属性让游戏的运行独立于帧率。**

* `Time.fixedDeltaTime`
    执行物理计算以及其他固定帧率的更新的时间间隔（单位为秒）。
    **建议使用 `Time.deltaTime` 来获取帧执行间隔**，因为在 FixedUpdate 或 Update 中使用 `Time.deltaTime` 会自动得到正确的帧执行间隔。
    **需要注意的是，`Time.fixedDeltaTime` 会受到 `Time.timeScale` 的影响。**

* `Time.timeScale`
    该属性用于控制时间的缩放，可以用来制作慢动作特效。
    **除了 `Time.realtimeSinceStartup` 之外，Time 类中的所有时间和时间差测量值都受到该属性的影响。**
    建议调低 `timeScale` 的同时也要对应调低 `Time.fixedDeltaTime` 的值。
    **当 `timeScale` 被设置为 0 时，FixedUpdate 方法不会被调用。**

### Data Types

![](media/15131774937303.png)

### Classes

// TODO: GO ON HERE

## Intermediate Gameplay Scripting

## Editor Scripting

## Community Posts

## Project Architecture

## Getting Started with Unity Development using Visual Studio

## Live Sessions on Scripting

## Live Session: Quiz Game

## Live Session: Localization Tools

## Live Session: Controlling Particles Via Script

## Live Session: Text Adventure Game

---

change log: 

	- 创建（2017-12-12）
	- 更新（2017-12-13）

---


