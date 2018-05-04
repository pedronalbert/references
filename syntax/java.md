# Java

## Declaration

```java
int foo = 42;
int[] numbers = new int[3];
int[] numbers = {1, 2, 3};
final int foo = 42; // Constant
```

## Built-in Types
```java
byte
short // 16-bits
int // 32-bit
long // 64-bit
float // 32-bit
double // 64-bit
boolean // 16-bit
char
```

## Control Flow
### If
```java
if (cond) {
  // ...
} else if (cond) {
  // ...
} else {
  // ...
}
```

### While

### For
```java
for (int i = 0; i <= n; i++) {
  // ...
}
```

### For each
```java
for (int client : clients) {
  // ...
}
```

```java
while(cond) {
  // ...
}
```

### Do..While
```java
do {
  // ...
} while(cond)
```

### Switch
```java
switch(foo) {
  case 1:
    // ...
    break;
  default:
    // ...
  break;
}
```

## Errors
### Handling
```java
try {
  // ...
} catch (Exception e) {
  // ...
} finally {
  // ...
}
```

### Custom Error
```java
public class MyError extends Exception {
  public MyError(String message) {
    super(message);
  }
}
```

## Classes
### Basic
```java
class Cat {
  public int age;
  static int foo;

  // Constructor
  public Cat() {
    // ...
  }

  // methods
  public void meow() {
    // ...
  }
}
```

### Inheritance
```java
class Mamal {
  public void eat() {
    // ...
  }
}

class Cat extends Mamal {
  @Overrida
  public void eat() {
    super();
  }
}
```

### Interfaces
```java
public interface Mamal {
  public void eat();
}

class Cat implements Mamal {
  // ...
}
```

### Abstracts
```java
public abstract class Animal {
  // Required Method
  abstract void eat();

  public void greet() {
    // ...
  }
}
```

### Final
```java
public final class Cat {
  // ...
}
```

### Nested
```java
```
