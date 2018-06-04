# vue小技巧（二）

## 1.vue filters 过滤器的使用：

过滤器，通常用于后台管理系统，或者一些约定的类型，过滤。Vue过滤器用法很简单。

在html模板中的两种方法：

```html
    // html
    {{ message | fillterTest }}
    // v-bind
    <div :id="message | filterTest">
```

组件中用法

```javascript
    export default {
        data() {
            return {
                message:1
            }
        },
        filters: {  
            filterTest(value) {
                // value在这里是message的值
                if(value===1){
                    return '最后输出这个值';
                }
            }
        }
    }
```

## 2.列表渲染相关

v-for循环绑定model:

input在v-for中可以像如下这么进行绑定

```javascript

        // 数据    
      data() {
          return{
           obj: {
              ob: "OB",
              koro1: "Koro1"
            },
            model: {
              ob: "默认ob",
              koro1: "默认koro1"
            }   
          }
      },
    // html模板
    <div v-for="(value,key) in obj">
       <input type="text" v-model="model[key]">
    </div>
      // input就跟数据绑定在一起了，那两个默认数据也会在input中显示
      
```

一段取值的v-for

如果我们有一段重复的html模板要渲染，又没有数据关联，我们可以

```
    <div v-for="n in 5">
        <span>这里会被渲染5次，渲染末班{{n}}</span>
    </div>
```


v-if尽量不要与v-for在同一节点使用

v-for 的优先级逼v-if更高,如果他们处于同一节点的话，那么每个循环都会运行一遍v-if，如果你想根据循环中的每一项数据来判断是否渲染，那么你这样做是对的

```html
    <li v-for="todo in todos" v-if="todo.type===1">
      {{ todo }}
    </li>

```

如果你想要根据某些条件跳过循环，而又跟将要渲染的每一项数据没有关系的话，你可以将v-if放在v-for的父节点：

```html

    // 根据elseData是否为true 来判断是否渲染，跟每个元素没有关系    
     <ul v-if="elseData">
      <li v-for="todo in todos">
        {{ todo }}
      </li>
    </ul>
    // 数组是否有数据 跟每个元素没有关系
    <ul v-if="todos.length">
      <li v-for="todo in todos">
        {{ todo }}
      </li>
    </ul>
    <p v-else>No todos left!</p>

```

#### date 2018.6.2