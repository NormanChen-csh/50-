# vue小技巧（五）

## 路由的项目启动页和404页面

实际上这也就是一个设置而已

```javascript

    export default new Router({
      routes: [
        {
          path: '/', // 项目启动页
          redirect:'/login'  // 重定向到下方声明的路由 
        },
        {
          path: '*', // 404 页面 
          component: () => import('./notFind') // 或者使用component也可以的
        },
      ]
    })

```

比如你的域名为:www.baidu.com

项目启动页指的是: 当你进入www.baidu.com，会自动跳转到login登录页。
404页面指的是: 当进入一个没有 声明/没有匹配 的路由页面时就会跳转到404页面。

比如进入www.baidu.com/testRouter,就会自动跳转到notFind页面。
当你没有声明一个404页面，进入www.baidu.com/testRouter，显示的页面是一片空白。

#### date 2018.6.5