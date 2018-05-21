# JS数组常用方法总结(一)

## 1. 所有子元素都改为‘a’

```javascript
arr.fill('a')
``` 

## 2. 后面八个元素 全部用{}代替

```javascript
[{a: 1}, {b: 2}, ...Array(8).fill({}, 0)]
```

## 3. 后面五个元素用{}代替，其他都是undefined

 ```javascript
[{a: 1}, {b: 2}, ...Array(8).fill({}, 0, 5)]
```

## 4. 如果数组中有一个元素的age > 20，返回true， 否则返回false

```javascript
arr.every(item => item.age > 20)
```

## 5. findIndex(),find()和filter()都是 匹配item;区别是find只找到第一个就停止，find返回的是符合的item。filter返回所有匹配的item组成的数组；findIndex返回的是item的index

## 6. lastIndexOf(), indexOf()和includes()都是检查是否存在某个item.

    区别 indexof无法判断NaN；includes可以
    indexof 找不到返回-1，找到返回index
    includes()直接返回true或false
    lastIndexOf()从字符后面开始查找，返回最后一个匹配的index，找不到 就返回-1

#### date 2018.5.21 18:00