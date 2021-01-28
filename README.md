# Unity Coding Standards

## Table of Contents

* [Naming conventions](#naming-conventions)
* [General C# file conventions](#general-c#-file-conventions)
* [Usings order](#usings-order)
* [Comments and documentation](#comments-and-documentation)

## Naming conventions

### Name formatting

Type         | Convention                      | Example
------------ | ------------------------------- | -----------------------
Namespace    | UpperCamelCase                  | `MyNamespace.SomeSystem`
Class        | UpperCamelCase                  | `MyClass`
Enum         | UpperCamelCase                  | `SomeEnumType`
Enum element | UpperCamelCase                  | `SomeEnumElement`
Property     | UpperCamelCase                  | `int MyProperty { get; }`
Field        | lowerCamelCase                  | `int myField`
Method       | UpperCamelCase                  | `MyMethod()`
Argument     | lowerCamelCase                  | `MyMethod(int arg)`
Coroutine    | Prefix "CO_" and UpperCamelCase | `CO_DoSomething()`

### Naming example

```csharp
namespace MyNamespace
{
    public class MyClass
    {
        public enum MyEnum {
            FirstElement,
            SecondElement
        }

        public int ExampleProperty { get => someField; }

        private int someField;

        public MyClass()
        {
            // ...
        }

        public MyMethod(int arg)
        {
            // ...
        }

        IEnumerator CO_DoSomething(int arg)
        {
            // ...
        }
    }
}
```

## General C# file conventions

```csharp
// Usings should come first
using System;
using System.Collection.Generic;
using System.Collections;
using UnityEngine;

// Put class definition inside an appropriate project namespace
namespace ThisProject.SomeSystem
{
    // Define only one class per file
    public class MyClass
    {
        // Constants
        private const float SOME_CONSTANT_VALUE = 10f;

        // Enum definitions
        public enum EnumExample {
            FirstElement,
            SecondElement,
            ...
        }

        // Properties
        public int SomeField { get => someField; }

        // Fields
        private int someField;

        // Constructors
        public MyClass()
        {
            ...
        }

        // Public methods
        public void MyPublicMethod()
        {
            ...
        }

        // Private methods
        private void Initialize()
        {
            ...
        }

        // Helper functions
        private int HelperFunction()
        {
            ...
        }
    }
}
```

## Usings order

```csharp
// 1. System namespaces
using System;
using System.Collections;
using System.Collections.Generic;
// 2. Unity libraries
using UnityEngine;
using UnityEngine.Events;
// 3. Third-Party Plugins
using ExampleCompany;
using OtherCompany.BoostedInspector;
// 4. Utility Libraries
using MyLib;
using MyLib.DebugUtilities;
using MyOtherLib.Patterns;
// 5. Project
using ThisProject;
using ThisProject.Audio;
using ThisProject.Combat;

// 6. Type aliases
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
