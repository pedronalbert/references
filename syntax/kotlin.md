# Kotlin
<!-- TOC -->

- [Kotlin](#kotlin)
  - [Declaration](#declaration)
  - [Built-in Types](#built-in-types)
  - [Packages](#packages)
    - [Declaration](#declaration-1)
    - [Import](#import)
  - [Arrays](#arrays)
  - [Functions](#functions)
    - [Declaration](#declaration-2)
    - [Inline Return](#inline-return)
    - [Named Arguments](#named-arguments)
  - [Control Flow](#control-flow)
    - [If](#if)
    - [When](#when)
    - [For](#for)
    - [While](#while)
  - [Classes](#classes)
    - [Instanciate](#instanciate)
    - [Properties](#properties)
      - [Getters & Setters](#getters--setters)
    - [Constructor](#constructor)
      - [Primary Constructor](#primary-constructor)
      - [Secondary Constructor](#secondary-constructor)
    - [Inheritance](#inheritance)
    - [Override Methods](#override-methods)
    - [Override Properties](#override-properties)
      - [Override on Constructor](#override-on-constructor)
    - [Nested Classes](#nested-classes)
    - [Inner Classes](#inner-classes)
    - [Interface](#interface)
    - [Extensions Functions](#extensions-functions)
    - [Data Classes](#data-classes)
    - [Generics](#generics)

<!-- /TOC -->
## Declaration
```kotlin
// Mutables
var n: Int = 42

// No mutables
val n: Int = 42

// Nullable
var n: Int? = 42
```

## Built-in Types
```kotlin
Double
Float
Long
Int
Short
Char
```

## Packages
### Declaration
```kotlin
package foo.Bar
```

### Import
```kotlin
import foo.Bar
import foo.Bar as Kar
import foo.*
```

## Arrays
```kotlin
```

## Functions
### Declaration
```kotlin
fun sum(a: Int, b: Int): Int {
  return a + b
}
```

### Inline Return
```kotlin
fun sum(a: Int, b: Int) = a + b
```

### Named Arguments
```kotlin
sum(b = 4)
```

## Control Flow
### If
```kotlin
if (condition) {
  // ...
} else {
  // ...
}

// Inline
val foo = if (a < b) a else b

// Blocked Expression
val max = if (a > b) {
  a
} else {
  b
}
```

### When
```kotlin
when (foo) {
  42 -> a //...
  43, 44 -> b // Multiple
  in 1..10 -> // Use in
  is String -> // Use is
  parseInt(s) -> // Expressions
  else -> {
    // Block Expression
  }
}

// Direct Booleans
when {
  x.isOdd() ->
  x.isEven() ->
  else ->
}
```

### For
```kotlin
for (cat: Cat in cats) {
  // ...
}
```

### While
```kotlin
while (condition) {
  // ...
}

do {
  // ...
} while (condition)
```

## Classes

```kotlin
class Pug {
  // ...
}
```

### Instanciate
> There is no `new` keyword in Kotlin
```kotlin
pepe = Pug()
```

### Properties
```kotlin
class Pug {
  val name: String = "pepe"
}
```

#### Getters & Setters
```kotlin
class Pug {
  val name: String
    get() {
      // ...
    }
    set(value) {
      // ...
    }
}
```
### Constructor

#### Primary Constructor
```kotlin
class Pug(name: String = "Pepe") {
  init {
    // Constructr code
  }
}
```

#### Secondary Constructor
> If the class has a primary constructor, each secondary constructor needs to delegate to the primary constructor
```kotlin
class Pug(name: String) {
  constructor(name: String, parent: Pug): this(name) {
    parent.children.add(this)
  }
}
```

### Inheritance
> All classes are final on kotlin by default, for inheritance requires de `open` keyword
```kotlin
open class Dog

class Pug : Dog {
  // ...
}
```
### Override Methods
> Requires `open` keyword on parent method
```kotlin
class Pug: Dog {
  override fun greet() {
    super.f() // Call to parent
    super<Dog>.f() // Call to specific parent
  }
}
```

### Override Properties
> Requires `open` keyword on parent propery
```kotlin
class Pug: Dog {
  override val name: String = "pepe"
}
```

#### Override on Constructor
```kotlin
class Pug(override val name: String)
```

### Nested Classes
```kotlin
class Outer {
    private val bar: Int = 1
    class Nested {
        fun foo() = 2
    }
}

val demo = Outer.Nested().foo() // == 2
```

### Inner Classes

```kotlin
class Outer {
    private val bar: Int = 1
    inner class Inner {
        fun foo() = bar
    }
}

val demo = Outer().Inner().foo() // == 1
```

### Interface
```kotlin
interface Animal {
  fun f()
}

class Pug : Animal {
  // ...
}
```

### Extensions Functions
```kotlin
class Dog {
  // ...
}

fun Dog.f() {
  // ...
}
```

### Data Classes
```kotlin
data class Pug(val name: String = "Pepe")
```

### Generics
```kotlin
class Box<T>(t: T) {
  val value = t;
}
```