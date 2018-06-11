# JS知识（一）

## 函数的三种定义方法

1. 函数声明  
2. 函数表达式
3. 构造函数

三种方法的对比

1. 函数声明有预解析，而且函数声明的优先级高于变量
2. 使用function构造函数定义函数的方式是一个函数表达式，这种方式会导致解析两次代码，影响性能。第一次解析常规的Javascript代码，第二次解析传入构造函数的字符串

## ES5中函数的四种调用

### 1.函数调用模式

    包括函数名（）和匿名函数调用，this指向window

```javascript
    function getSum() {
        console.log(this) //window
    }
    getSum()
    (function() {
        console.log(this) //window
    })()
    var getSum=function() {
        console.log(this) //window
    }
    getSum()

```

### 2.方法调用

```javascript
    var objList = {
        name: 'methods',
        getSum: function() {
            console.log(this) //objList对象
        }
    }

    objList.getSum()
```

### 3.构造器调用

new 构造函数名（），this指向构造函数

### 间接调用

利用call和apply来实现，this就是call和apply对应的第一个参数，如果不传值或者第一个值为null，undefined时this指向window

```javascript
    function foo() {
        console.log(this);
    }
    foo.apply('我是apply改变的this值');//我是apply改变的this值
    foo.call('我是call改变的this值');//我是call改变的this值

```

#### date 2018.6.9