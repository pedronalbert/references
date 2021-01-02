# Symbols
- Symbols are inivisible to loops

```js
const mySymbol = Symbol('foo');
```

# Iterators
```js
class Users {
  [Symbol.iterator]() {
    let i = 0;

    return {
      next() {
        if (hasNext()) {
          return { done: false, value: currentValue },
        }

        return { done: true };
      }
    }
  }
}
```

## To remember

> ¿En que consiste y cuando ocurre el hoisting?

