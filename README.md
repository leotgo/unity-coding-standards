# Unity3D Coding Standards

An attempt at documenting my own coding standards, a composition of coding standards acquired from multiple Unity developers across the community.

## References

* [Microsoft Naming Guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines)
* [raywenderlich/c-sharp-style-guide](https://github.com/raywenderlich/c-sharp-style-guide)
* [Unreal coding standards](https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)

## Table of Contents

* [General C# file conventions](#general-c#-file-conventions)
* [Naming conventions](#naming-conventions)
* [Usings order](#usings-order)
* [Comments and documentation](#comments-and-documentation)

## General C# file conventions

### Rules of thumb

* Library usings should be the first lines of a file, followed by *typedef*-like usings;
* Put class definition inside an appropriate namespace;
* Prefer defining only one class per file;
* File name should be the same as the class name.

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

In **private** methods, prefer the following order:

1. Initialization methods
2. Core functionality methods
3. Helper or explanatory methods

### MonoBehaviour example

```csharp
using System;
using System.Collection.Generic;
using System.Collections;
using UnityEngine;

using SomeDataType = Dicitonary<Object, int>;

namespace MyCompany.MyGame.SomeSystem
{
    public class MyClass : MonoBehaviour, ISomethingInterface
    {
        public class Data
        {
            ...
        }

        private const float SOME_CONSTANT_VALUE = 10f;

        public enum EnumExample {
            FirstElement,
            SecondElement,
            ...
        }

        public SomeDataType SomeProperty { get => someField; }

        private SomeDataType someField;
 
        public MyClass()
        {
            ...
        }

        private void Awake()
        {
            ...
        }

        public void MyPublicMethod()
        {
            ...
        }

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
namespace TowerDefenseGame.Combat
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

An interface for something that can be a physics target for a *Motor*, such as the `PlayerMotor`:

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
