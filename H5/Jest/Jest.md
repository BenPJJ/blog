# Jest

## 测试异步函数

### 1. 回调函数

```js
function fetchData(call) {
  setTimeout(() => {
    call('butter');
  }, 1000);
}

describe('async function', () => {
  test('the data is peanut butter', (done) => {
    function callback(data) {
      expect(data).toBe('butter')
      done()
    }
    fetchData(callback);
  })
})
```

### 2. Promise

``` js
function fetchData(call) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject('butter')
    }, 1000);
  })
}

// 1. 原生promise
describe('async function', () => {
  test('the data is peanut butter', () => {
    expect.assertions(1);
    return fetchData().catch(data => {
    	expect(data).toBe('butter')
    });
  })
})

// 2. jest20.00+，提供的语法糖 resloves、rejects
describe('async function', () => {
  test('the data is peanut butter', () => {
    expect.assertions(1);
    return expect(fetchData()).rejects.toBe('butter')
  })
})

// 3. jest20.00+，async、await搭配语法糖resloves、rejects
describe('async function', () => {
  test('the data is peanut butter', async () => {
    expect.assertions(1);
    await expect(fetchData()).rejects.toBe('butter')
  })
})
```

