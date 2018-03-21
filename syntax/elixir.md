# Elixir
<!-- TOC -->

- [Elixir](#elixir)
  - [DataTypes](#datatypes)
    - [Strings](#strings)
    - [Lists](#lists)
    - [Map](#map)
  - [Pattern Matching](#pattern-matching)
  - [Control Flow](#control-flow)
    - [Comprehension](#comprehension)
    - [Case](#case)
    - [Cond](#cond)
    - [if and unless](#if-and-unless)
    - [With](#with)
  - [Modules](#modules)
    - [Attributes](#attributes)
    - [Importing](#importing)
    - [Aliasing](#aliasing)
  - [Functions](#functions)
    - [Pattern Matching](#pattern-matching-1)
    - [Guards](#guards)
  - [Structs](#structs)
  - [Documentation](#documentation)
  - [Macros](#macros)
    - [Use clause](#use-clause)
  - [Behaviours](#behaviours)
  - [Protocols](#protocols)
    - [Available Types](#available-types)
  - [Errors](#errors)
    - [Custom Error](#custom-error)
    - [Raising](#raising)
  - [Concurrency](#concurrency)
    - [Spawn](#spawn)
    - [Tasks](#tasks)
      - [Waiting Tasks](#waiting-tasks)
  - [Testing](#testing)
    - [Fixtures](#fixtures)
  - [Tools](#tools)

<!-- /TOC -->
## DataTypes

```elixir
0b1010 # Binaries
0o755 # Octals
0xFF  # Hex
6.57e-10 # Exp
"Hello" # String (bytes)
'Hełło' # Charlist (codepoints)
[1, 2, 3] # List
[juan: 23, david: 21] # Keyword List
{ :foo, "bar" } # Tuple
%{ foo: "var" } # Map
<< 0, 1, 2 >> # Binaries
```
### Strings
```elixir
"Hello #{world}" # Interpolation
"Hello" <> "World" # Concatenate
```

### Lists
```elixir
++ # Concatenate
-- # Substract
hd # Head
tl # Tail
```

### Map
```elixir
# Declaration
%{ :a => 1, :b => 2 } == %{ a: 1, b: 2 }

# Access
map.a == Map.fetch(map, :a)

# Update
%{ map | :b => 3 }
```

## Pattern Matching
```elixir
# Lists
[head | tail] = [1, 2, 3]

# Pin Operator
^x = 2
```

## Control Flow

### Comprehension
```elixir
for x <- list, do: x * x

# Multiples Lists
for x <- list1, y <- list, do: x * y

# Filters
for x <- list, x >= 0, do: x * x

# Change return value
for x <- list, into: %{}, do: { x, String.uppercase(x) }
```

### Case
```elixir
case foo do
  pattern ->
    # Code
  pattern when bar > 0 ->
    # Extra condition
  ^bar ->
    # Pattern exisiting variable
  _ ->
    # Any
end
```

### Cond
```elixir
cond do
  2 + 2 == 5 ->
    # ...
  2 * 2 == 3 ->
    # ...
  true ->
    # ...
end
```

### if and unless
```elixir
if cond do
  # ...
else
  # ...
end

unless cond do
  # ...
end
```

### With
```elixir
with {:ok, user} <- create_user,
  {:ok, comments} <- get_comments(user)
do
  {:ok, comments}
else
  {:error, reason} -> {:error, reason}
end
```

## Modules
```elixir
defmodule MyMath do
  # ...functions
end
```

### Attributes
```elixir
defmodule MyMod do
  @foo "value"
end
```

### Importing
```elixir
import MyModule, only: [greet: 1]
import MyModule, only: :macros
import MyModule, except: [greet: 1]
import MyModule, except: :functions
```

### Aliasing
```elixir
alias MyModule.NestedModule.Parser [, as: Parser]

# Multiples
alias MyModule.NestedModule.{Parser, Runner}
```

## Functions

```elixir
#Basic
def square(x \\ 2) do
  x * 2
end

#Private
defp square(x) do
  x * 2
end

# Inline
def square(x), do: x * 2

#Anonymous
fn x -> x * 2 end
```

### Pattern Matching
```elixir
def (pattern) do
  # ...
end
```

### Guards
```elixir
def square(x) when x > 0 do
  x * x
end

fn
  x, y when x > 0 -> x / 0
  x, y -> x + y
end
```

## Structs
```elixir
# Declaration
defmodule User
  @enforce_keys [:age]  # Required keys
  defstruct [:name, :age] # Without default values
  defstruct name: "John", age: 12
end

# Usage
%User{name: "Pedro", age: 23}
```

## Documentation
```elixir
@moduledoc
@vs
@doc
@spec my_function(number()) :: float()
```

## Macros
> When we pass parameters to a macro, Elixir doesn't evaluate them, instead, it passes them as tuples representing 
so we need unquote the params

```elixir
defmacro double(n) do
  quote do
    unquote(n) * 2
  end
end
```

### Use clause
```elixir
defmodule Entity do
  defmacro __using__(_opts) do
    quote do
      # to insert in use clause
    end
  end
end

defmodule User do
  use Entity # used __using__ macro
end
```

## Behaviours
A behaviours is like a Interface on Java we need to specify as @callback on parent for require the implementation on child modules
```elixir
defmodule Entity do
  @callback fetchable? :: boolean
end

defmodule User do
  @behaviour Entity

  def fetchable?, do: true # Now is required due to behaviour
end
```

## Protocols
Protocols is the base of polymorphic functiosn on Elixir
```elixir
defprotocol Inspect do
  def inspect(thing, opts)
end

defimpl Inspect, for: PID do
  def inspect(pid, _opts) do
    # ...
  end
end

defimpl Inspect, for: [List, Tuple] do
  def inspect(_any, _opts) do
    # ...
  end
end
```

### Available Types
Any Atom BitString Float Function Integer List Map PID Port Record Reference Tuple

## Errors
```elixir
try do
  # ...
rescue
  e in RuntimeError -> # ...
  e -> # ...
after
  # ...
end
```

### Custom Error
```elixir
defmodule MyError do
  defexception message: "Example error",
    other: false

  def full_message(me) do
    "Full message..."
  end
end
```

### Raising
```elixir
raise RuntimeError, message: "Overrido"
```

## Concurrency

### Spawn
```elixir
spawn(Module, :method, [args])
spawn_link(Module, :method, [args])
```


### Tasks
```elixir
Task.async(fn -> IO.puts "Hi" end)
Task.async(Module, :function, [args])
```

#### Waiting Tasks
```elixir
worker = Task.async(...)

results = Task.await(worker)
```


## Testing
```elixir
defmodule CatTest do
  use ExUnit.Case

  test "Should be true" do
    assert Cat.has_hat
  end

  test "Should be false" do
    refute Cat.has_hat
  end
end
```

### Fixtures
```elixir
defmodule CatTest do
  describe "Should" do
    setup do
      [ numbers: [1, 2, 3] ]
    end

    test "Testing" do
      asset fixtures.numbers == [1, 2, 3]
    end
  end
end
```

## Tools
[ExCheck](https://github.com/parroty/excheck)
