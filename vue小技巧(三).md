# vue小技巧（三）

# 深度watch与watch立即触发回调

watch很多人都在用，但是这个watch中的这两个选项deep、immediate，或许不是很多人都知道。

在选项参数中指定deep: true，可以监听对象中属性的变化

选项：immediate

在选项参数中指定 immediate:true 将立即以表达式的当前值触发回调，也就是默认触发一次

```javascript

    watch: {
        obj: {
          handler(val, oldVal) {
            console.log('属性发生变化触发这个回调',val, oldVal);
          },
          deep: true // 监听这个对象中的每一个属性变化
        },
        step: { // 属性
          //watch
          handler(val, oldVal) {
            console.log("默认触发一次", val, oldVal);
          },
          immediate: true // 默认触发一次
        },
      }
```

#### date 2018.6.3