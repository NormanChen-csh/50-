# JS高级技巧学习

***

## 困扰很久的类型检测

1. 先讲两种常用的typeof和instanceof
    ```bash
    在tyoeof null === 'object' 最开始JavaScript是由一个表示类型的标签和实际数据值表示的。对象的类型标签是0.由于null代表的是空指针（大多数平台下值为0x00），因此，null的类型标签页成为了0，typeof null就错误返回了object。

    但是在浏览器中，我们的脚本可能需要在多个窗口之间进行交互。多个窗口意味着多个全局环境，不同的全局环境拥有不同的全局对象，从而拥有不同的内置类型构造函数。这可能会引发一些问题。
    ```
2. 讲讲**Object.prototype.toString**
    ```javascript
    var toString = Object.prototype.toString

    toString.call(new Date); // [object Date]
    toString.call(new String); // [object String]
    toString.call(Math); // [object Math]
    toString.call(/s/); // [object RegExp]
    toString.call([]); // [object Array]

    //Since JavaScript 1.8.5
    toString.call(undefined); // [object Undefined]
    toString.call(null); // [object Null]
    ```

## 函数节流 场景是需要一次性调用多次函数，比如下拉刷新这种

节流的目的是防止某些操作执行的太快。比如在调整浏览器大小的时候回发出onsize事件，如果在其内部进行一些DOM操作，这种高频率的更改可能会使浏览器崩溃。为了避免这种情况，可以采取函数节流的方式。

```javascript
function throttle(method, context) {
    clearTimeout(method.tId)
    method.tId = setTimeout(function () {
        method.call(context)
    }, 100)
}
```

这里接受两个参数，要执行的函数，执行的环境。执行时先清除之前的定时器，然后将当前定时器赋值给放的tId,之后调用call来圈定函数的执行环境。

一个例子。

```javascript
function resizeDiv () {
    let div = document.getElementById('div')
    div.style.height = div.offsetWidth + 'px'
}

window.onresize = function () {
    throttle(resizDiv)
}
```

#### date 2018.5.15 14:00