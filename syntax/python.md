# Python
<!-- TOC -->

- [Python](#python)
  - [Declaration](#declaration)
  - [Build-in Types](#build-in-types)
    - [String](#string)
    - [Lists](#lists)
      - [Slicing](#slicing)
      - [Concatenate](#concatenate)
      - [Existence](#existence)
  - [Functions](#functions)
    - [Declaration](#declaration-1)
    - [Keyword Arguments](#keyword-arguments)
    - [Lambdas](#lambdas)
  - [Modules](#modules)
    - [Import](#import)
  - [Control Flow](#control-flow)
    - [If](#if)
    - [For](#for)
    - [While](#while)
  - [Classes](#classes)
    - [Instanciate](#instanciate)
    - [Properties](#properties)
    - [Constructor](#constructor)
    - [Getter & Setter](#getter--setter)
    - [Static Method](#static-method)
    - [Inheritance](#inheritance)
    - [Override Method](#override-method)
  - [Errors](#errors)
    - [Try/Except](#tryexcept)
    - [Custom Error](#custom-error)
    - [Raising](#raising)
    - [With](#with)

<!-- /TOC -->
## Declaration
```python
n = 42
```

## Build-in Types
```python
True or False # Boolean
"Hello" # String
'Hello' # String
[1, 2, 3] # Lists
(1, 2, 3) # Tuple
{"foo": "var"} # Hash
```

### String
```python
"You name is %s, age %d" % (name, age)
"Your name is {}, age {}".format(name, age)
"Your name is {name}, age {age}".format(name="Bob", age=42)
```

### Lists

#### Slicing
> Slicing is exclusive
```python
list[1:42]
list[::2] # Every 2
```

#### Concatenate
```python
list1 + list2
```

#### Existence
```python
name in list # => True/False
```

## Functions

### Declaration
```python
def add(x, y, *args, **kwargs):
  # ...
```

### Keyword Arguments
```python
def add(x, y = 42, z = 32):
  return x * y * z

add(25, z = 42)
```

### Lambdas
```python
lambda x, y: x * y
```

## Modules

### Import
```python
import fibo
import fibo as fib
from fibo import calc, avg
```

## Control Flow

### If
```python
if condition:
  # ...
elif condition:
  # ...
else:
  # ...
```

### For
```python
for user in users:
  # ...

for i in range(5)
for i in range(2, 4)
```

### While
```python
while condition:
  #...
```

## Classes

### Instanciate
```python
pepe = Pug(args)
```

### Properties
```python
class Pug:
  name = "pepe"
```

### Constructor
```python
class Pug:
  name = "pepe"

  def __init__(self, name):
    self.name = name
```

### Getter & Setter
```python
class Pug:
  age = 10

  @property
  def age(self):
    self.age

  @age.setter
  def age(self, age):
    self.age = age * 4
```

### Static Method
```python
class Pug:
  @staticmethod
  def clone_from(adn):
    # ...
```

### Inheritance
```python
class Pug(Dog):
  pass
```

### Override Method
```python
class Pug(Dog):
  def greet(self):
    super().greet()
```
## Errors

### Try/Except
```python
try:
  # ...
except CatError as e:
  # ...
except (CatError, DogError):
  # ..
else
  # ...
finally:
  # ...
```

### Custom Error
```python
class MyError(Exception):
  def __init__(self, other, message):
    self.other = other
    self.message = message
```

### Raising
```python
raise MyError('Hi There')
```

### With
```python
with open("file.text)
```