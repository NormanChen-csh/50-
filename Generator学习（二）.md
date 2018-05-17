# Generator基础知识学习二

## yield语法

yield的语法有点像return，但是，return是在函数调用结束后返回结果的
并且在调用return之后不会执行其他任何的操作

```javascript
function method (a) {
  let b = 5
  return a + b
  // 下边的两句代码永远不会执行
  b = 6
  return a * b
}

method(6) // 11
method(6) // 11
```

### 而yield的表现则不一样

```javascript
function * yieldMethod(a) {
  let b = 5
  yield a + b
  // 在执行第二次`next`时，下边两行则会执行
  b = 6
  return a * b
}

const gen = yieldMethod(6)
gen.next().value // 11
gen.next().value // 36
```

### yield*

yield*用来将一个Generator放到另一个Generator函数中执行。
有点像[...]的功能：

```javascript
function * gen1 () {
  yield 2
  yield 3
}

function * gen2 () {
  yield 1
  yield * gen1()
  yield 4
}

let gen = gen2()

gen.next().value // 1
gen.next().value // 2
gen.next().value // 3
gen.next().value // 4
```

### yield的返回值

yield是可以接收返回值的，返回值可以在后续的代码被使用
一个诡异的写法

```javascript
function * generator (num) {
  return yield yield num
}

let gen = generator(1)

console.log(gen.next())  // {value: 1, done: false}
console.log(gen.next(2)) // {value: 2, done: false}
console.log(gen.next(3)) // {value: 3, done: true }
```

我们在调用第一次next时候，代码执行到了yield num，此时返回num
然后我们再调用next(2)，代码执行的是yield (yield num)，而其中返回的值就是我们在next中传入的参数了，作为yield num的返回值存在。
以及最后的next(3)，执行的是这部分代码return (yield (yield num))，第二次yield表达式的返回值。

#### data 2018.5.17 20:00