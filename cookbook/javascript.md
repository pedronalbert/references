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

## Singleton
```js
const Singleton = function () {
  return {
    getInstance: function() {
      return this;
    }
  }
}
```

El exports siempre se cache por lo cual si devolvemos una instancia hará como singleton
```js
module.exports = new Cat();
```

## Streams

### Writable
```js
const { Writable } = require('stream');

const ws = new Writable({
  write(chunk, encoding, cb) {
    // ...
  }
})

// Métodos
ws.write(data)
ws.end()
```

### Readable
> Se da como terminada la lectura cuando se inserta un `null`

```js
const { Readable } = require('stream');

const rs = new Readable({
  read(size) {

  }
});

// Metodos

rs.push(data);
```
