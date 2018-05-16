# Generator 基础知识学习

***

## 基本解释：**Generator 是一个可以被暂停的函数，并且何时恢复，由调用方法决定。**

## 关键API： next()、yield

通过调用yield可以暂停函数的执行，再调用next()方法可以让函数继续执行，达到一个随时控制的效果。

## Generator基本语法

声明Generator函数有很多种途径，最重要的一点就是，**在关键字后面添加一个‘*’**

```javascript
function * generator () {}
function* generation () {}
function *generation () {}

let generator = function * () {}
let generator = function* () {}
let generator = function *() {}

class MyClass {
  * generator() {}
  *generator2() {}
}

const obj = {
  *generator() {}
  * generator() {}
}

//错误示例
let generator = *() => {}
let generator = ()* => {}
let generator = (*) => {}

// generator函数貌似不支持ES6箭头函数语法
```

### 初始化以及复用

一个Genrator函数通过调用两次方法，将会生成两个完全独立的**状态机**。所以，保存当前的Generator对象很重要。

```javascript
function * generator (name = 'unknown') {
    yield `Your name: ${name}`
}

const gen1 = generator()
const gen2 = generator('Chisfee')

gen1.next() //{ value: Your name: unknown    , done: false}
gen2.next() // { value: Your name: Chisfee, done: false}
```

### Method: next()

最常用的next()方法，无论何时调用它，都会得到下一次输出的返回对象（在代码执行完成后的调用将会始终返回{value: undefined, done: true}）

next 总会返回一个对象，包含两个属性值
value： yield关键字后边表达式的值
done: 如果一斤更没有yield关键字了，最会返回true

```javascript
function * generator () {
    yield 5
    return 6
}

const gen = generator ()

console.log(gen.next()) // {value: 5, done: false}
console.log(gen.next()) // {value: 6,done: true}
console.log(gen.next()) // {value: undefined, done: true}
console.log(gen.next()) // {value: undefined, done: true} --- 后续再调用都是这个结果

// yield调用一次就失效
```

### 作为迭代器使用

Generator 函数是一个可以迭代的，所以，我们可以直接通过for of 来使用它。

```javascript
function * generator () {
    yield 1
    yield 2
    return 3
}

for (let item of generator()) {
    item
}

// 1
// 2
```

*return* 不参与迭代
迭代会执行所有的yield，也就是说，在迭代后的Generator对象将不会再返回任何有效的价值

## Method: throw()

在调用throw() 后同样会终止所有的yield执行，同事会抛出一个异常，需要通过try-catch来接收：

```javascript
function * generator () {
    yield 1
    yield 2
    yield 3
}

const gen = generator()

gen.throw('error text') // Error: error text
gen.next() // {value: undefined, done: true}

//不会有返回值
```