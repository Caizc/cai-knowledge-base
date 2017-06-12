# Useful Stuff in Unity Scripting

## GameObject

* `public static Object Instantiate(Object original, Vector3 position, Quaternion rotation);`

    [Object.Instantiate](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html)

> Clones the object original and returns the clone.

```c#
using UnityEngine;
using System.Collections;

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

## CharacterController

[CharacterController](https://docs.unity3d.com/ScriptReference/CharacterController.html)

> A CharacterController allows you to easily do movement constrained by collisions without having to deal with a rigidbody.
> A CharacterController is not affected by forces and will only move when you call the Move funtion. It will then carry out the movement but be constrained by collisions.

* `public CollisionFlags Move(Vector3 motion);`

    [CharacterController.Move](https://docs.unity3d.com/ScriptReference/CharacterController.Move.html)

> A more complex move function taking absolute movement deltas.

## Debug

[Debug](https://docs.unity3d.com/ScriptReference/Debug.html)

* `public static void Log(object message);`

Logs message to the Unity Console.

```c#
 // Message with a link to an object.
Debug.Log("Hello", gameObject);
// Message using rich text.
Debug.Log("<color=red>Fatal error:</color> AssetBundle not found");
```

-------

* int Random.Range(int min, int max)
Returns a random integer number between min [inclusive] and max [exclusive] (Read Only). min: max:

* Quaternion Quaternion.identity
The identity rotation (Read Only).

* Transform Transform.parent
The parent of the transform.

* [SerializeField]

* using System.Collections.Generic;

* OnEnable()

* Reset()

* public static float GetAxisRaw(string axisName)

-------

> www link prefix：
> https://docs.unity3d.com

> local link prefix：
> file:///Applications/Unity/Unity.app/Contents/Documentation/en

---

change log: 

	- 创建（2017-06-09）
	- 更新（2017-06-12）

---

