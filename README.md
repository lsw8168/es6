# ES6: es6 sample

## Resources

## Memoization

ES6 메모제이션

```js
const memoize = (fn) => {
  let cache = {}, key;
  return (...args) => {
    key = JSON.stringify(args);
    return cache[key] || (cache[key] = fn.call(null, ...args));
  }
};

let pureAdd = (x, y) => x + y; // pure function
let memoizedAdd = memoize(pureAdd); // memoized pure function

memoizedAdd(3, 4)
memoizedAdd(3, 4)
memoizedAdd(3, 4)
```
