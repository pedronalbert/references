# Jest

## Matchers

### Modifiers
```js
.not
.resolves
.rejects
```

### ToBe
```js
.toBe(value)
.toBeTruthy()
.toBeFalsy()
.toBeNull()
.toBeUndefined()
.toBeNaN()
.toBeDefined()
.toBeCloseTo(number, numDigits?)
.toBeGreaterThan(number | bigint)
.toBeGreaterThanOrEqual(number | bigint)
.toBeLessThan(number | bigint)
.toBeLessThanOrEqual(number | bigint)
.toBeInstanceOf(Class)
```

### Comparative
```js
.toHaveLength(number)
.toHaveProperty(keyPath, value?)
.toContain(item)
.toContainEqual(item)
.toEqual(value)
.toMatch(regexpOrString)
.toMatchObject(object)
.toMatchSnapshot(propertyMatchers?, hint?)
.toMatchInlineSnapshot(propertyMatchers?, inlineSnapshot)
.toStrictEqual(value)
```

### Functions

```js
.toHaveBeenCalled()
.toHaveBeenCalledTimes(number)
.toHaveBeenCalledWith(arg1, arg2, ...)
.toHaveBeenLastCalledWith(arg1, arg2, ...)
.toHaveBeenNthCalledWith(nthCall, arg1, arg2, ....)
.toHaveReturned()
.toHaveReturnedTimes(number)
.toHaveReturnedWith(value)
.toHaveLastReturnedWith(value)
.toHaveNthReturnedWith(nthCall, value)
.toThrow(error?)
.toThrowErrorMatchingSnapshot(hint?)
.toThrowErrorMatchingInlineSnapshot(inlineSnapshot)
```

## Mocking

### Functions
```js
const mockedFn = jest.fn(x => x)
```

### Modules
```js
```

### API
```js
mockFn.getMockName()
mockFn.mock.calls // [['arg1', 'arrg2'], ['arg1', 'arg2']]
mockFn.mock.results // [{ type: 'return', value: 'foo'}, { type: throw: value: error }]
mockFn.mock.instances
mockFn.mockClear()
mockFn.mockReset()
mockFn.mockRestore()
mockFn.mockImplementation(fn)
mockFn.mockImplementationOnce(fn)
mockFn.mockName(value)
mockFn.mockReturnThis()
mockFn.mockReturnValue(value)
mockFn.mockReturnValueOnce(value)
mockFn.mockResolvedValue(value)
mockFn.mockResolvedValueOnce(value)
mockFn.mockRejectedValue(value)
mockFn.mockRejectedValueOnce(value)
```