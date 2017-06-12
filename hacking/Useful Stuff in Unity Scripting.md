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

-------

* int Random.Range(int min, int max)
Returns a random integer number between min [inclusive] and max [exclusive] (Read Only). min: max:

* OnEnable()

* Reset()

* public static float GetAxisRaw(string axisName)

-------

> www link prefix：https://docs.unity3d.com
> local link prefix：file:///Applications/Unity/Unity.app/Contents/Documentation/en

---

change log: 

	- 创建（2017-06-09）
	- 更新（2017-06-12）

---

