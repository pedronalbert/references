# Javascripot

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
