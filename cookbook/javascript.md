# Javascripot

## Trampoline
[Post](https://blog.logrocket.com/using-trampolines-to-manage-large-recursive-loops-in-javascript-d8c9db095ae3)
```js
const trampoline = fn => (...args) => {
  let result = fn(...args);

  while (typeof result === 'function') {
    result = result();
  }

  return result;
}
```

## functors
```js
const Functor = value => ({
  map: fn => Functor(fn(value)),
  valueOf: () => value, // used for arithmetic operators
  toString: () => `Functor(${value})`,
  constructor: Functor,
});
```

## Functional Mixin
```js
const flying = (obj) => {
  let isFlying = false;

  return {
    ...obj,

    fly() {
      isFlying = true;

      return this;
    },
  };
};
```
