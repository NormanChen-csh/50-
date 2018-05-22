# JS数组常用方法总结（二）

## 对比数组方法是否会改变源数组

## （一）影响源数组的几个方法

### 新增-1

    let arr = [1,2,3,4];
    arr.push(5)//[1, 2, 3, 4, 5];
    arr.unshift(0)//[0, 1, 2, 3, 4, 5]

### 删除-1

    1.  pop()、shift()
        let arr = [1,2,3,4];
        l(arr.pop());//4 取到最后一个
        l(arr)//[1,2,3] 原数组被改变
        l(arr.shift());//1 取到第一个
        l(arr)//[2,3] 原数组被改变

    2.  splice()
        let arr = ['a','b','c','d'];
        arr.splice(1,2)//1代表从索引为1的数开始('b'),2代表删除('b','c')这两个元素,也就实现了删除这个目的
        l(arr)["a","d"]

### 替换-1

    1. splice()
        let arr = ['a','b','c','d'];
        l(arr.splice(1,2,'e','f'))//["b", "c"]
        l(arr)//["a", "e", "f", "d"]

## （二）不影响源数组的几个方法

### 新增-2

    1. concat()
        let arr = [1, 2, 3, 4]
        arr.concat(5)
        l(arr) //[1,2,3,4]
    2. (...)
        let arr1 = [1, 2, 3, 4]
        let arr2 = [...arr1, 5]
        l(arr2) //[1, 2, 3, 4, 5]
        l(arr2) //[1, 2, 3, 4, 5]

### 删除-2

    1. Array.filter()
        let arr = [1, 2, 3, 4]
        l(arr.filter(e => e !== 3)) //[1, 2, 4] e代表arr中的每一项
        l(arr) //[1, 2, 3, 4]源数组未改变
    2. Array.slice()
        let arr = ['a', 'b', 'c', 'd']
        l(arr.slice(1, 2)) //['b']
        l(arr) //["a", "b", "c", "d"]

### 替换-3

    1. map()
    let arr = ['a','b','c','d'];
    let arr1= arr.map(item => {
        if (item == 'b') {
            item = 'f'
        }
        return item
    } )
    l(arr1)//["a", "f", "c", "d"]
    l(arr)//['a','b','c','d']