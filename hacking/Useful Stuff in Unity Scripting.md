# Useful Stuff in Unity Scripting

## GameObject

[GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html)

> Base class for all entities in Unity scenes.

-------

[Object.Instantiate](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html)
    
* `public static Object Instantiate(Object original, Vector3 position, Quaternion rotation);`

> Clones the object original and returns the clone.

```c#
public class ExampleClass : MonoBehaviour {
    public Rigidbody projectile;
    void Update() {
        if (Input.GetButtonDown("Fire1")) {
            Rigidbody clone;
            clone = Instantiate(projectile, transform.position, transform.rotation) as Rigidbody;
            clone.velocity = transform.TransformDirection(Vector3.forward * 10);
        }
    }
}
```

-------

[GameObject.GetComponent](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)

* `public Component GetComponent<T>();`

> Returns the component of Type type if the game object has one attached, null if it doesn't.

**See Also: GetComponents, GetComponentInParent, GetComponentInChildren.**

```c#
public class GetComponentExample : MonoBehaviour
{
    void Start()
    {
        HingeJoint hinge = gameObject.GetComponentInParent<HingeJoint>();
        if (hinge != null)
            hinge.useSpring = false;
    }
}
```

## Transform

[Transform](https://docs.unity3d.com/ScriptReference/Transform.html)

> Position, rotation and scale of an object.

-------

[Transform.parent](https://docs.unity3d.com/ScriptReference/Transform-parent.html)

* `public Transform parent;`

> The parent of the transform.

-------

[Transform.position](https://docs.unity3d.com/ScriptReference/Transform-position.html)

* `public Vector3 position;`
    
> The position of the transform in world space.

-------

[Transform.rotation](https://docs.unity3d.com/ScriptReference/Transform-rotation.html)

* `public Quaternion rotation;`

> The rotation of the transform in world space stored as a Quaternion.

-------

[Transform.Translate](https://docs.unity3d.com/ScriptReference/Transform.Translate.html)

* `public void Translate(Vector3 translation, Space relativeTo = Space.Self);`

> Moves the transform in the direction and distance of translation.

```c#
public class ExampleClass : MonoBehaviour {
    void Update() {
        transform.Translate(Vector3.forward * Time.deltaTime);
        transform.Translate(Vector3.up * Time.deltaTime, Space.World);
    }
}
```

-------

[Transform.Rotate](https://docs.unity3d.com/ScriptReference/Transform.Rotate.html)

* `public void Rotate(Vector3 eulerAngles, Space relativeTo = Space.Self);`

> Applies a rotation of eulerAngles.z degrees around the z axis, eulerAngles.x degrees around the x axis, and eulerAngles.y degrees around the y axis (in that order).

```c#
public class ExampleClass : MonoBehaviour
{
    void Update()
    {
        // Rotate the object around its local X axis at 1 degree per second
        transform.Rotate(Vector3.right * Time.deltaTime);

        // ...also rotate around the World's Y axis
        transform.Rotate(Vector3.up * Time.deltaTime, Space.World);
    }
}
```

-------

[Transform.localScale](https://docs.unity3d.com/ScriptReference/Transform-localScale.html)

* `public Vector3 localScale;`

> The scale of the transform relative to the parent.

```c#
public class ExampleClass : MonoBehaviour
{
    void Example()
    {
        // Widen the object by 0.1
        transform.localScale += new Vector3(0.1F, 0, 0);
    }
}
```

-------

[Transform.localEulerAngles](https://docs.unity3d.com/ScriptReference/Transform-localEulerAngles.html)

* `public Vector3 localEulerAngles;`

> The rotation as Euler angles in degrees relative to the parent transform's rotation.
> The x, y, and z angles represent a rotation z degrees around the z axis, x degrees around the x axis, and y degrees around the y axis (in that order).
> **Only use this variable to read and set the angles to absolute values. Don't increment them, as it will fail when the angle exceeds 360 degrees. Use Transform.Rotate instead.**

## Space

[Space](https://docs.unity3d.com/ScriptReference/Space.html)

> The coordinate space in which to operate.

-------

* `Space.World`
* `Space.Self`

## Rigidbody

[Rigidbody](https://docs.unity3d.com/ScriptReference/Rigidbody.html)

> Control of an object's position through physics simulation.
> **Adding a Rigidbody component to an object will put its motion under the control of Unity's physics engine.** Even without adding any code, a Rigidbody object will be pulled downward by gravity and will react to collisions with incoming objects if the right Collider component is also present.
>**In a script, the FixedUpdate function is recommended as the place to apply forces and change Rigidbody settings (as opposed to Update, which is used for most other frame update tasks).**

-------

[Rigidbody.freezeRotation](https://docs.unity3d.com/ScriptReference/Rigidbody-freezeRotation.html)

* `public bool freezeRotation;`

> Controls whether physics will change the rotation of the object.
> **If freezeRotation is enabled, the rotation is not modified by the physics simulation. This is useful for creating first person shooters, because the player needs full control of the rotation using the mouse.**

## Collider

[Collider](https://docs.unity3d.com/ScriptReference/Collider.html)

> A base class of all colliders.
> **If the object with the Collider needs to be moved during gameplay then you should also attach a Rigidbody component to the object. The Rigidbody can be set to be kinematic if you don't want the object to have physical interaction with other objects.**

**See Also: BoxCollider, SphereCollider, CapsuleCollider, MeshCollider, PhysicMaterial.**

## CharacterController

[CharacterController](https://docs.unity3d.com/ScriptReference/CharacterController.html)

> A CharacterController allows you to easily do movement constrained by collisions without having to deal with a rigidbody.
> A CharacterController is not affected by forces and will only move when you call the Move funtion. It will then carry out the movement but be constrained by collisions.

-------

[CharacterController.Move](https://docs.unity3d.com/ScriptReference/CharacterController.Move.html)

* `public CollisionFlags Move(Vector3 motion);`

> A more complex move function taking absolute movement deltas.

## Quaternion

[Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html)

> Quaternions are used to represent rotations.

-------

[Quaternion.identity](https://docs.unity3d.com/ScriptReference/Quaternion-identity.html)

* `public static Quaternion identity;`

> The identity rotation (Read Only).
> This quaternion corresponds to "no rotation" - the object is perfectly aligned with the world or parent axes.

## Input

[Input](https://docs.unity3d.com/ScriptReference/Input.html)

> Use this class to read the axes set up in the `Input Manager`, and to access multi-touch/accelerometer data on mobile devices.
> To read an axis use `Input.GetAxis` with one of the following default axes: "`Horizontal`" and "`Vertical`" are mapped to joystick, A, W, S, D and the arrow keys. "`Mouse X`" and "`Mouse Y`" are mapped to the mouse delta. "`Fire1`", "`Fire2`" "`Fire3`" are mapped to Ctrl, Alt, Cmd keys and three mouse or joystick buttons. New input axes can be added in the Input Manager.

Note also that the `Input` flags are not reset until "`Update()`", so its suggested you make all the `Input Calls` in the `Update` Loop.

-------

[Input.GetAxis](https://docs.unity3d.com/ScriptReference/Input.GetAxis.html)

* `public static float GetAxis(string axisName);`

> Returns the value of the virtual axis identified by axisName.
> The value will be in the range -1...1 for keyboard and joystick input. If the axis is setup to be delta mouse movement, the mouse delta is multiplied by the axis sensitivity and the range is not -1...1.

This is frame-rate independent; you do not need to be concerned about varying frame-rates when using this value.

```c#
public class ExampleClass : MonoBehaviour {
    public float speed = 10.0F;
    public float rotationSpeed = 100.0F;
    void Update() {
        float translation = Input.GetAxis("Vertical") * speed;
        float rotation = Input.GetAxis("Horizontal") * rotationSpeed;
        translation *= Time.deltaTime;
        rotation *= Time.deltaTime;
        transform.Translate(0, 0, translation);
        transform.Rotate(0, rotation, 0);
    }
}
```

-------

[Input.GetAxisRaw](https://docs.unity3d.com/ScriptReference/Input.GetAxisRaw.html)

* `public static float GetAxisRaw(string axisName);`

> Returns the value of the virtual axis identified by axisName with no smoothing filtering applied.
> The value will be in the range -1...1 for keyboard and joystick input. Since input is not smoothed, keyboard input will always be either -1, 0 or 1. This is useful if you want to do all smoothing of keyboard input processing yourself.

```c#
public class ExampleClass : MonoBehaviour {
    void Update() {
        float speed = Input.GetAxisRaw("Horizontal") * Time.deltaTime;
        transform.Rotate(0, speed, 0);
    }
}
```

-------

[Input.GetButton](https://docs.unity3d.com/ScriptReference/Input.GetButton.html)

* `public static bool GetButton(string buttonName);`

> Returns true while the virtual button identified by buttonName is held down.
> Think auto fire - this will return true as long as the button is held down.

Use this only when implementing events that trigger an action, eg, shooting a weapon. Use `GetAxis` for input that controls continuous movement.

```c#
// Instantiates a projectile every 0.5 seconds, if the Fire1 button (default is Ctrl) is pressed.
public class ExampleClass : MonoBehaviour
{
    public GameObject projectile;
    public float fireDelta = 0.5F;

    private float nextFire = 0.5F;
    private GameObject newProjectile;
    private float myTime = 0.0F;

    void Update()
    {
        myTime = myTime + Time.deltaTime;
        if (Input.GetButton("Fire1") && myTime > nextFire)
        {
            nextFire = myTime + fireDelta;
            newProjectile = Instantiate(projectile, transform.position, transform.rotation) as GameObject;

            // create code here that animates the newProjectile

            nextFire = nextFire - myTime;
            myTime = 0.0F;
        }
    }
}
```

-------

[Input.GetButtonDown](https://docs.unity3d.com/ScriptReference/Input.GetButtonDown.html)

* `public static bool GetButtonDown(string buttonName);`

> Returns true during the frame the user pressed down the virtual button identified by buttonName.
> You need to call this function from the `Update` function, since the state gets reset each frame. It will not return true until the user has released the key and pressed it again.

Use this only when implementing action like events IE: shooting a weapon.
Use `Input.GetAxis` for any kind of movement behaviour.

```c#
public class ExampleClass : MonoBehaviour
{
    public GameObject projectile;
    void Update()
    {
        if (Input.GetButtonDown("Fire1"))
            Instantiate(projectile, transform.position, transform.rotation);
    }
}
```

## Time

[Time](https://docs.unity3d.com/ScriptReference/Time.html)

-------

[Time.deltaTime](https://docs.unity3d.com/ScriptReference/Time-deltaTime.html)

* `public static float deltaTime;`

> The time in seconds it took to complete the last frame (Read Only).

Use this function to make your game frame rate independent.

If you add or subtract to a value every frame chances are you should multiply with `Time.deltaTime`. When you multiply with `Time.deltaTime` you essentially express: I want to move this object 10 meters per second instead of 10 meters per frame.

When called from inside MonoBehaviour's `FixedUpdate`, returns the fixed framerate delta time.

Note that you should not rely on `Time.deltaTime` from inside `OnGUI` since OnGUI can be called multiple times per frame and deltaTime would hold the same value each call, until next frame where it would be updated again.

```c#
public class ExampleClass : MonoBehaviour {
    void Update() {
        float translation = Time.deltaTime * 10;
        transform.Translate(0, 0, translation);
    }
}
```

## Debug

[Debug](https://docs.unity3d.com/ScriptReference/Debug.html)

> Class containing methods to ease debugging while developing a game.

-------

* `public static void Log(object message);`

> Logs message to the Unity Console.

```c#
// Message with a link to an object.
Debug.Log("Hello", gameObject);
// Message using rich text.
Debug.Log("<color=red>Fatal error:</color> AssetBundle not found");
```

## Mathf

[Mathf](https://docs.unity3d.com/ScriptReference/Mathf.html)

> A collection of common math functions.

-------

[Mathf.Clamp](https://docs.unity3d.com/ScriptReference/Mathf.Clamp.html)

* `public static float Clamp(float value, float min, float max);`

> Clamps a value between a minimum float and maximum float value.

```c#
public class ExampleClass : MonoBehaviour {
    void Update() {
        transform.position = new Vector3(Mathf.Clamp(Time.time, 1.0F, 3.0F), 0, 0);
    }
}
```

## Attributes

> Attributes are markers that can be placed above a class, property or function in a script to indicate special behaviour.

-------

[SerializeField](https://docs.unity3d.com/ScriptReference/SerializeField.html)

* `SerializeField`

> Force Unity to serialize a private field.

```c#
public class SomePerson : MonoBehaviour
{
    //This field gets serialized because it is public.
    public string name = "John";

    //This field does not get serialized because it is private.
    private int age = 40;

    //This field gets serialized even though it is private
    //because it has the SerializeField attribute applied.
    [SerializeField]
    private bool hasHealthPotion = true;

    void Update()
    {
    }
}
```

-------

[HideInInspector](https://docs.unity3d.com/ScriptReference/HideInInspector.html)

* `HideInInspector`

> Makes a variable not show up in the inspector but be serialized.

```c#
public class ExampleClass : MonoBehaviour {
    [HideInInspector]
    public int p = 5;
}
```

## Execution Order of Event Functions

[Execution Order of Event Functions](https://docs.unity3d.com/Manual/ExecutionOrder.html)

### Editor

* **Reset:** `Reset` is called to initialize the script’s properties when it is first attached to the object and also when the `Reset` command is used.

### First Scene Load

> These functions get called when a scene starts (**once for each object in the scene**).

* **Awake:** This function is always called before any `Start` functions and also just after a prefab is instantiated. (If a `GameObject` is inactive during start up `Awake` is not called until it is made active.)

* **OnEnable:** (only called if the Object is active): This function is called just after the object is enabled. This happens when a `MonoBehaviour` instance is created, such as when a level is loaded or a `GameObject` with the script component is instantiated.

* **OnLevelWasLoaded:** This function is executed to inform the game that a new level has been loaded.

> Note that for objects added to the scene, the `Awake` and `OnEnable` functions for all scripts will be called before `Start`, `Update`, etc are called for any of them. Naturally, this cannot be enforced when an object is instantiated during gameplay.

### Before the first frame update

* **Start:** Start is called before the first frame update only if the script instance is enabled.

> For objects added to the scene, the `Start` function will be called on all scripts before `Update`, etc are called for any of them. Naturally, this cannot be enforced when an object is instantiated during gameplay.

### In between frames

* **OnApplicationPause:** This is called at the end of the frame where the pause is detected, effectively between the normal frame updates. One extra frame will be issued after `OnApplicationPause` is called to allow the game to show graphics that indicate the paused state.

### Update Order

> When you’re keeping track of game logic and interactions, animations, camera positions, etc., there are a few different events you can use. The common pattern is to perform most tasks inside the `Update` function, but there are also other functions you can use.

* **FixedUpdate:** `FixedUpdate` is often called more frequently than `Update`. It can be called multiple times per frame, if the frame rate is low and it may not be called between frames at all if the frame rate is high. All physics calculations and updates occur immediately after `FixedUpdate`. When applying movement calculations inside `FixedUpdate`, you do not need to multiply your values by `Time.deltaTime`. This is because `FixedUpdate` is called on a reliable timer, independent of the frame rate.
* **Update:** `Update` is called once per frame. It is the main workhorse function for frame updates.
* **LateUpdate:** `LateUpdate` is called once per frame, after `Update` has finished. Any calculations that are performed in `Update` will have completed when `LateUpdate` begins. A common use for `LateUpdate` would be a following third-person camera. If you make your character move and turn inside `Update`, you can perform all camera movement and rotation calculations in `LateUpdate`. This will ensure that the character has moved completely before the camera tracks its position.

### Rendering

// TODO

### Coroutines

// TODO

### When the Object is Destroyed

* **OnDestroy:** This function is called after all frame updates for the last frame of the object’s existence (the object might be destroyed in response to `Object.Destroy` or at the closure of a scene).

### When Quitting

// TODO

### Script Lifecycle Flowchart

> The following diagram summarises the ordering and repetition of event functions during a script’s lifetime.

![](media/14972781767662.jpg)

-------

* int Random.Range(int min, int max)
Returns a random integer number between min [inclusive] and max [exclusive] (Read Only). min: max:

-------

> www link prefix：https://docs.unity3d.com
> 
> local link prefix：file:///Applications/Unity/Unity.app/Contents/Documentation/en

---

change log: 

	- 创建（2017-06-09）
	- 更新（2017-06-13）

---

