## ES6: es6 sample

### Memoization

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



### Generator

ES9 제너레이터


비동기 처리
```js
const fetch = require('node-fetch');

function getUser(genObj, username) {
  fetch(`https://api.github.com/users/${username}`)
    .then(res => res.json())
    // ① 제너레이터 객체에 비동기 처리 결과를 전달한다.
    .then(user => genObj.next(user.name));
}

// 제너레이터 객체 생성
const g = (function* () {
  let user;
  // ② 비동기 처리 함수가 결과를 반환한다.
  // 비동기 처리의 순서가 보장된다.
  user = yield getUser(g, 'jeresig');
  console.log(user); // John Resig

  user = yield getUser(g, 'ahejlsberg');
  console.log(user); // Anders Hejlsberg

  user = yield getUser(g, 'ungmo2');
  console.log(user); // Ungmo Lee
}());

// 제너레이터 함수 시작
g.next();


```

### async/awit (ES7)

```js
const fetch = require('node-fetch');

// Promise를 반환하는 함수 정의
function getUser(username) {
  return fetch(`https://api.github.com/users/${username}`)
    .then(res => res.json())
    .then(user => user.name);
}

async function getUserAll() {
  let user;
  user = await getUser('jeresig');
  console.log(user);

  user = await getUser('ahejlsberg');
  console.log(user);

  user = await getUser('ungmo2');
  console.log(user);
}

getUserAll();
```
