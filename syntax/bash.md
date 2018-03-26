# Bash
<!-- TOC -->

- [Bash](#bash)
  - [DataTypes](#datatypes)
  - [Arguments](#arguments)
  - [Sustitution](#sustitution)
  - [Control Flow](#control-flow)
    - [If](#if)
    - [Case](#case)
    - [While](#while)
    - [Until](#until)
    - [For](#for)
  - [Functions](#functions)

<!-- /TOC -->

```sh
expr # Arithmetic expression
```

## DataTypes
```sh
(foo var) # Arrays
```

## Arguments
```sh
$# # Numero de argumentos
$? # Estado de salida del ultimo comando
$$ # PID
```

## Sustitution
```sh
$(command)
`command`
```

## Control Flow
### If
```sh
if [ command ]; then
  # ...
else
  # ...
elif [ command ]; then
  # ...
fi
```

### Case
```sh
case $FOO in
  pattern )
    # ...
  ;;
  * )
    # ...
  ;;
esac
```

### While
```sh
while [ command ]
do
  # ...
done
```

### Until
```sh
until [ command ]
do
  #...
done
```

### For
```sh
for i in foo
do
  # ...
done

for (( i = 0 ; i <= 10 ; i ++ ))
do
  # ...
done

# Arrays
for foo in "${myArray[@]}"
do
  # ...
done
```

## Functions
```sh
name() {
  # ...
}

name foo # Calling with params
```
