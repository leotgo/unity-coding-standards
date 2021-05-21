# Unity3D Coding Standards

An attempt at documenting a composition of coding standards acquired from multiple game developers across the community.

## Table of Contents

1. [File layout](#file-layout)
2. [Naming conventions](#naming-conventions)
3. [Code documentation](#code-documentation)
4. [References](#references)

## File layout

### General rules

* Library usings should be the first lines of a file, followed by *typedef*-like usings;
* Put class definition inside an appropriate namespace;
* Prefer defining only one class per file;
* File name should be the same as the class name.

### Usings order

Usings should be defined in the following order:

 1. System or .NET libraries
 2. Unity libraries
 3. Third-Party plugins (asset store)
 4. Your own utility libraries
 5. Project namespaces
 6. Type name aliases

 All namespace categories should be blocked together, without separating with spaces or comments.
 An exception to this is *typedef*-like usings, which should be separated from library usings with an empty line.

**Example:**

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
using ExampleCompany;
using OtherCompany.BoostedInspector;
using MyUtilityLib;
using MyUtilityLib.DebugUtilities;
using MyOtherLib.Patterns;
using ThisProject;
using ThisProject.Audio;
using ThisProject.Combat;

using EntityPrefabMap = Dictionary<EntityType,GameObject>;
```

### Class definition order

Define a class in the following order:

 1. Nested classes
 2. Constants
 3. Enums
 4. Properties
 5. Fields
 6. Constructors (if applicable)
 7. Unity Messages
 8. Public methods
 9. Private methods

**Example:**

```csharp
public class MyClass : MonoBehaviour
{
    private class MyNestedClass
    {
        ...
    }

    private const int SOME_CONSTANT = 1;

    public enum SomeEnum {
        FirstElement,
        SecondElement
    }

    public int SomeProperty { get => someField; }

    private int someField;

    private void Start()
    {
        ...
    }

    public void SomePublicMethod()
    {
        ...
    }

    private void SomePrivateMethod()
    {
        ...
    }
}
```

### Private methods order

Prefer the following order:

1. Initialization methods
2. Core functionality methods
3. Helper or explanatory methods

**Example:**

```csharp
// Initialization
private void Initialize()
{
    ...
}

// Core functionality
private void Move(Vector3 direction)
{
    ...
}

// Helper
private bool CheckIfPositionIsWalkable(Vector3 position)
{
    ...
}
```

## Naming conventions

### Casing

* Identifiers for classes, methods, namespaces, enums, properties, attributes and coroutines are `PascalCase`
* Identifiers for fields, local variables, parameters are `camelCase`
* Constants are written in `UPPER_CASE`. Example: `DEFAULT_EXPONENT`
* The convention for casing is unaffected by modifiers such as `public`, `private`, `protected`, `static` or `readonly`
* Acronyms should be treated as words and are written in `PascalCase`. Examples: `XmlFormatter`, `AiBehaviour`, `UiElement`

#### Examples

* Namespaces and classes

```csharp
namespace Xml
{
    public class XmlFormatter
    {
        ...
    }
}
```

* Fields

```csharp
public  int id;
private InputHandler input;
private float health;
```

* Properties

```csharp
public float Health
{
    get
    {
        return health;
    }
    set
    {
        health = value;
    }
}
```

* Methods and parameters

```csharp
public void Move(Vector3 movement)
```

* Constants

```csharp
public const int MAX_SCENE_OBJECTS = 256;
```

* Attributes

```csharp
[ConsoleAttribute] public float gameSpeed;
```

### Identifier naming

#### Namespaces

The identifier should briefly describe the "system" or set of definitions contained in the library.

Examples:

```csharp
namespace Utilities.Debug
```

```csharp
namespace TowerDefenseGame.Combat
```

```csharp
namespace TowerDefenseGame.UI
```

#### Classes

The class name should briefly describe its responsibilities or data. Prefer including the suffix *"Base"* in abstract classes where applicable.

Examples:

* A class responsible for performing movement on the player character's transform:

```csharp
class PlayerMotor
```

* An abstract class for implementing behaviors for AI Agents:

```csharp
abstract class AiBehaviourBase
```

#### Interfaces

Interfaces should include the prefix "I". The interface name should briefly describe the purpose of its members or the components it interacts with.

Examples:

```csharp
interface IMotorTarget
```

```csharp
interface IUiElement
```

#### Methods

Method names should describe the effect caused by the method, or the return value if the method has no effect.

Examples:

* A method that performs movement on the player character. Tipically, the name for this type of method should be a verb.

```csharp
public void Move(Vector3 movement)
```

* A method that converts radians to degrees. Notice that while the return type is a float, the name of the method helps to understand how the value should be interpreted.

```csharp
private float RadianToDegrees(float radians)
```

* A method to determine if a position in the world can be traversed by the player. Once again, the name for the method explains how the return value should be interpreted.

```csharp
private bool IsPositionWalkable(Vector3 position)
```

#### Coroutines

Coroutines are written with the prefix 'CO_', and the rest of its identifier should follow the same rules as methods.

Examples:

```csharp
IEnumerator CO_SpawnPlayer(int playerId)
```

## Code documentation

### In-code documentation

Write self-documenting code when possible. Avoid overly abbreviated variables which don't have semantic value for the reader.

```csharp
// Bad:
p = p + v * dt;
```

```csharp
// Good:
position = position + velocity * deltaTime;
```

You can also use explanatory variables to avoid writing complicated and unreadable lines:

```csharp
// Bad:
pos = Vector3.Lerp(targetEnemy.position, GetComponent<AutoMovementController>().targetWaypoint.nextPosition, time / max);
```

```csharp
// Good:
var waypoint = player.GetComponent<AutoMovementController>().targetWaypoint;
var startPosition = targetEnemy.position;
var finalPosition = waypoint.nextPosition;
var lerpPoint = time / maxMovementTime;
position = Vector3.Lerp(startPosition, finalPosition, lerpPoint);
```

### Comments

Write useful comments. Avoid being redundant with what the code is telling the reader. Instead, disclose valuable information that might not be directly perceivable.

```csharp
// Bad:
// increment player id
playerId++;
```

```csharp
// Good:
// We know that a new player has joined, generate a new identifier.
playerId++;
```

Do not comment bad or unreadable code. Prefer rewriting it instead.

```csharp
// Bad:
// Increase current position by the velocity scaled by deltaTime to perform movement.
p = p + v * dt;
```

```csharp
// Good:
position = position + velocity * deltaTime;
```

Do not contradict the code!

```csharp
// Bad:
// Health value should be between 0 and 100
private int health;

...

this.health = 150;
```

```csharp
// Good:
// Default Health values should be between 0 and 100.
private int health;

...

// Apply the temporary health buff from consuming potion.
this.health = 150;
```

## References

* [Microsoft Naming Guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines)
* [raywenderlich/c-sharp-style-guide](https://github.com/raywenderlich/c-sharp-style-guide)
* [Unreal coding standards](https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)