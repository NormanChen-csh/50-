# vue小技巧（四）

## 1.以下情况下不要使用箭头函数

    1. 不应该使用箭头函数来定义一个生命周期方法
    2. 不应该使用箭头函数来定义 method 函数
    3. 不应该使用箭头函数来定义计算属性函数
    4. 不应该对 data 属性使用箭头函数
    5. 不应该使用箭头函数来定义 watcher 函数

```javascript
        // 上面watch的栗子：
    handler:(val, oldVal)=> { // 可以执行
     console.log("默认触发一次", val, oldVal);
   },
   // method：
     methods: {
        plus: () => { // 可以执行
          // do something
        }
      }
   // 生命周期:
     created:()=>{ // 可以执行
       console.log('lala',this.obj) 
      }

```

这些能执行

但是：

箭头函数绑定了父级作用域的上下文，this将不会按照期望指向Vue实例。

也就是说，你不能使用this来访问你组件中的data数据以及method方法

this将会指向undefined

## 2.路由懒加载写法

```javascript

    // 我所采用的方法，个人感觉比较简洁一些，少了一步引入赋值。
    const router = new VueRouter({
      routes: [
        path: '/app',
        component: () => import('./app'),  // 引入组件
      ]
    })
    // Vue路由文档的写法:
    const app = () => import('./app.vue') // 引入组件
    const router = new VueRouter({
      routes: [
        { path: '/app', component: app }
      ]
    })

```

文档的写法在于问题在于：如果我们的路由比较多的话，是不是要在路由上方引入赋值十几行组件？

第一种跟第二种方法相比就是把引入赋值的一步，直接写在component上面，本质上是一样的。两种方式都可以的，大家自由选择哈。

#### date 2018.6.4