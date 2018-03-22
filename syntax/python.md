# Python

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
{"foo": "var"} # Hash
```

### String
```python
"You name is %s, age %d" % (name, age)
"Your name is {}, age {}".format(name, age)
"Your name is {name}, age {age}".format(name="Bob", age=42)
```

### Lists
```python
# Slicing
list[1:42]
list[::2] # Slice every 2

# Concatenate
list1 + list2

# Exist
name in list # => True/False
```

## Functions

### Declaration
```python
def add(x, y, *args, **kwargs):
  # ...
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

```python
class Pug(Dog):
  name = "pepe"

  # Constructor
  def __init__(self, namme):
    # ...

  # Instance Method
  def jump(self)
    # ...

  # Static Method
  @staticmethod
  def clone(adn)
    # ...

  # Override Method
  def poop(self):
    super().poop()

  # Getter
  @property
  def age(self):
    # ...

  # Setter
  @age.setter
  def age(self, age):
    self.age = age

# Instanciate Class
pepe = Pug()
```

## Errors

### Try
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

### With
```python
with open("file.text)
```