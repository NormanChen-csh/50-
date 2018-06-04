# Vue小技巧

## 1.组件style的scoped

在vue的组件中动态创建的DOM，在style中添加的样式不会生效，原因是动态创建的DOM没有添加scoped这个标识。

## 解决方法

去掉scoped。还可以动态添加style

    newDOM.style.height = '100px'

## 2.Vue数组/对象更新 视图不更新

```javascript

    data() { // data数据
        return {
          arr: [1,2,3],
          obj:{
              a: 1,
              b: 2
          }
        };
      },
   // 数据更新 数组视图不更新
    this.arr[0] = 'OBKoro1';
    this.arr.length = 1;
    console.log(arr);// ['OBKoro1'];
    // 数据更新 对象视图不更新
    this.obj.c = 'OBKoro1';
    delete this.obj.a;
    console.log(obj);  // {b:2,c:'OBKoro1'}

```

**由于js的限制，Vue 不能检测以上数组的变动，以及对象的添加/删除，很多人会因为像上面这样操作，出现视图没有更新的问题。**

## 解决方法

1. this.$set(你要改变的数组/对象，你要改变的/位置，你要改什么value)

```
    this.$set(this.arr, 0, "OBKoro1"); //改变数组
    this.$set(this.obj, "c", "OBKoro1"); // 改变对象
```

2. 数组原生方法触发视图更新

Vue可以检测到数组变化的，数组原生方法

```
    splice()、push()、pop()、shift()、unshift()、sort()、reverse()
```

意思是使用这些方法不用我们再进行额外的操作，视图自动进行更新

推荐使用splice方法会比较号自定义，因为slice可以在数组的任何位置进行删除/添加操作

3. 替换数组/对象

比方说： 你想遍历这个数组/对象，对每个元素进行处理，然后出发视图更新

```javascript

    // 文档中的栗子: filter遍历数组，返回一个新数组，用新数组替换旧数组
    example1.items = example1.items.filter(function (item) {
      return item.message.match(/Foo/)
    })

```

举一反三： 可以先把这个数组/对象保存在一个变量中，然后对这个变量进行遍历，等遍历结束后在用变量替换对象/数组

并不会重新渲染整个列表:

Vue 为了使得 DOM 元素得到最大范围的重用而实现了一些智能的、启发式的方法，所以用一个含有相同元素的数组去替换原来的数组是非常高效的操作。

#### date 2018.6.1