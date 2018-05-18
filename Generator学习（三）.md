# Generator基础知识学习（三）

## generator 实际使用场景

上边的所有示例都是建立在已知次数的Generator函数上的，但如果你需要一个未知次数的Generator，仅需要创建一个无限循环就够了。

### 一个简单的随机数生成

随机数获取

```javascript
function * randomGenerator (...randoms) {
  let len = randoms.length
  while (true) {
    yield randoms[Math.floor(Math.random() * len)]
  }
}

const randomeGen = randomGenerator(1, 2, 3, 4)

randomeGen.next().value // 返回一个随机数
```

## 代替一些递归的操作

那个最著名的斐波那契数，基本上都会选择使用递归来实现
但是再结合着Generator以后，就可以使用一个无限循环来实现了：

```javascript
function * fibonacci(seed1, seed2) {
  while (true) {
    yield (() => {
      seed2 = seed2 + seed1;
      seed1 = seed2 - seed1;
      return seed2;
    })();
  }
}

const fib = fibonacci(0, 1);
fib.next(); // {value: 1, done: false}
fib.next(); // {value: 2, done: false}
fib.next(); // {value: 3, done: false}
fib.next(); // {value: 5, done: false}
fib.next(); // {value: 8, done: false}
```

## 与async/await的结合

如果是写前端的童鞋，基本上都会遇到处理分页加载数据的时候
如果结合着Generator+async、await，我们可以这样实现：

```javascript
async function * loadDataGenerator (url) {
  let page = 1

  while (true) {
    page = (yield await ajax(url, {
      data: page
    })) || ++page
  }
}

// 使用setTimeout模拟异步请求
function ajax (url, { data: page }) {
  return new Promise((resolve) => {
    setTimeout(_ => {
      console.log(`get page: ${page}`);
      resolve()
    }, 1000)
  })
}

let loadData = loadDataGenerator('get-data-url')

await loadData.next()
await loadData.next()

// force load page 1
await loadData.next(1)
await loadData.next()

// get page: 1
// get page: 2
// get page: 1
// get page: 2
```

这样我们可以在简单的几行代码中实现一个分页控制函数了。
如果想要从加载特定的页码，直接将page传入next即可。

#### date 2018.5.18 23:00