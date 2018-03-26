# Ruby
<!-- TOC -->

- [Ruby](#ruby)
  - [DataTypes](#datatypes)
    - [Arrays](#arrays)
      - [Slicing](#slicing)
  - [Modules](#modules)
    - [Include](#include)
    - [Extend](#extend)
  - [Control Flow](#control-flow)
    - [If](#if)
    - [Unless](#unless)
    - [Case](#case)
    - [For](#for)
    - [Times](#times)
    - [While](#while)
    - [Begin](#begin)
    - [Guard](#guard)
  - [Functions](#functions)
    - [Lambdas](#lambdas)
    - [Aliases](#aliases)
  - [Blocks](#blocks)
  - [Classes](#classes)
    - [Instanciate](#instanciate)
    - [Properties](#properties)
    - [Constructor](#constructor)
    - [Getter & Setter](#getter--setter)
    - [Attr Accessors](#attr-accessors)
    - [Inheritance](#inheritance)
    - [Override Methods](#override-methods)
  - [Errors](#errors)
    - [Begin/Rescue](#beginrescue)
    - [CustomError](#customerror)

<!-- /TOC -->

## DataTypes
```ruby
42 # Int
42.24 # Floats
[1, 2, 3] # Arrays
{foo: "var"} # Hahes
```

### Arrays
#### Slicing
```ruby
list[1..3] # Inclusive
list[1,3] # Exclusive
```

## Modules
```ruby
module Users
  # ...
  def self.list
    # users
  end
end

# Deep modules
module Entities::Users
```

### Include
>Add module's methods as instance methods
```ruby
module Animal
  def greet
    puts self.class
  end
end

class Cat
  include Animal
end

Cat.new.greet # => Cat
```

### Extend
>Add module's methods as class methods
```ruby
module Animal
  def greet
    puts self.class
  end
end

class Cat
  extend Animal
end

Cat.greet
```

## Control Flow

### If

```ruby
if condition
  # ...
elsif condition
  # ...
else
  # ...
end
```

### Unless
```ruby
unless cnd
  # ...
end
```

### Case
```ruby
case foo
  when condition
    # ...
  when condition1, condition2
    # ...
  else
    # ...
end
```

### For
```ruby
for i in 1..5 do
  # ...
end
```

### Times
```ruby
5.times do
  # ...
end
```

### While
```ruby
while cnd do
  # ...
end
```

### Begin
```ruby
begin
  # ...
end while cnd
```

### Guard
```ruby
call_foo if cnd
call_foo unless cnd
```

## Functions
```ruby
def foo(a, b, *args)
  # ...
end
```

### Lambdas
```ruby
lmd = -> (name) { puts name }
```
### Aliases
```ruby
def foo()
  # ...
end

alias var foo
```

## Blocks
```ruby
def foo(&b)
  b.call()
end

def foo
  yield
end
```

## Classes

### Instanciate
```ruby
pepe = Pug.new(args)
```

### Properties
```ruby
class Pug
  @name = "default_name"
end
```

### Constructor
```ruby
class Pug
  def initialize(name) 
    @name = name
  end
end
```

### Getter & Setter
```ruby
class Pug
  # Getter
  def name
    @name
  end

  # Setter
  def name=(name) 
    @name = name
  end
end
```

### Attr Accessors
```ruby
attr_reader :name
attr_writer :name
attr_accessor :name
```

### Inheritance
```ruby
class Pug < Dog
end
```

### Override Methods
```ruby
class Pug < Dog
  def greet
    super 
    # ...
  end
end
```

## Errors

### Begin/Rescue
```ruby
begin
  raise UnknownError, 'Yep one error'
rescue UnknownError
  # ...
end
```

### CustomError
```ruby
class MyError < StandardError
  attr_reader :other_info

  def initialize(info)
    @other_info = info
  end
end
```
