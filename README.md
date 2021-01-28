# Unity3D Coding Standards

## Table of Contents

* [General C# file conventions](#general-c#-file-conventions)
* [Naming conventions](#naming-conventions)
  * [Name formatting](#name-formatting)
  * [Naming example](#naming-example)
* [Usings order](#usings-order)
* [Comments and documentation](#comments-and-documentation)

## General C# file conventions

```csharp
// Usings should come first
using System;
using System.Collection.Generic;
using System.Collections;
using UnityEngine;

using SomeDataType = Dicitonary<Object, int>;

// Put class definition inside an appropriate namespace
namespace MyCompany.MyGame.SomeSystem
{
    // Define only one class per file.
    // Put base class first, interfaces after.
    public class MyClass : MonoBehaviour, ISomethingInterface, IAnotherInterface
    {
        // 1. Nested classes
        public class Data
        {
            ...
        }

        // 2. Constants
        private const float SOME_CONSTANT_VALUE = 10f;

        // 3. Enums
        public enum EnumExample {
            FirstElement,
            SecondElement,
            ...
        }

        // 4. Properties
        public int SomeField { get => someField; }

        // 5. Fields
        private int someField;

        // 6. Constructors
        public MyClass()
        {
            ...
        }

        // 7. Unity Messages
        private void Awake()
        {
            ...
        }

        // 8. Public methods
        public void MyPublicMethod()
        {
            ...
        }

        // 9. Private methods
        private void Initialize()
        {
            ...
        }

        private void DoSomething()
        {
            ...
        }

        private int HelperFunction()
        {
            ...
        }
    }
}
```

## Naming conventions

### Namespaces

Namespaces are formatted in UpperCamelCase, with the exception of acronyms such as AI, UI, HUD.
The name should briefly describe the "system" or set of definitions contained in the library.

**Examples:**

```csharp
namespace Utilities.Debug
```

```csharp
namespace TowerDefenseGame.CombatSystem
```

```csharp
namespace TowerDefenseGame.UI
```

### Classes

Class names are formatted in UpperCamelCase. Acronyms can be included as a prefix or suffix.
The class name should briefly describe its responsibilities or data. Prefer including the suffix *"Base"* in abstract classes where applicable.

Examples:

A class responsible for performing movement on the player character's transform:

```csharp
class PlayerMotor
```

An abstract class for implementing behaviors for AI Agents:

```csharp
abstract class AIBehaviourBase
```

### Interfaces

Interfaces should include the prefix "I". The following words should be formatted in UpperCamelCase. Avoid using acronyms after the prefix, such as `IUIElement`. The interface name should briefly describe the semantics of the members and/or which components they are supposed to interact with.

Examples:

An interface for a GameObject that can be a physics target for a *Motor* type, such as a `PlayerMotor`:

```csharp
interface IMotorTarget
```

```csharp
```

### Nested Classes

WIP

### Enums

WIP

### Properties and Fields

WIP

### Methods

WIP

### Coroutines

WIP

### Arguments

WIP

## Usings order

Usings should be defined in the following order:

 1. System or .NET libraries
 2. Unity libraries
 3. Third-Party plugins (asset store)
 4. Your own utility libraries
 5. Project namespaces
 6. Type name aliases

 All namespace categories should be blocked together, without separating with spaces or comments.
 An exception to this is *typedef*-like usings, which should be separated from library usings with an empty line.

Example:

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

## Comments and documentation

Document public classes with XML comments.

```csharp
///<summary>
/// Base class for implementations of behaviors of AI Agents.
///</summary>
public class AIBehavior
{
    ...
}
```

WIP
