# vuex基本使用和相关规范

1. dispatch提交action,commit提交mutation。dispatch是异步，commit 是同步
2. 通过使用,import和mapActions 可以获取action的方法并且能够直接调用或重命名调用
3. 只允许通过mutation 来变更state的状态（内容）


### 官方Action介绍

[action介绍](https://vuex.vuejs.org/zh-cn/actions.html)

```js
	import {
        mapActions
    } from 'vuex'
    
    ...mapActions({
    	getListsData: 'getListsData'
    })
```
### 使用的相关小技巧

* 可以通过this.$store.state.这种方法取到state里面的值并进行修改（不推荐）
* dispatch和commit的时候，第二个参数可以带一个载荷，这是一个json，且不允许有第三个参数
* 一般将数据请求写在action中，如果对数据渲染有先后顺序的要求，可以将整个请求用promise return 
```js
    getShopData({ commit }, resData) {
    	return axios.post(url, resData).then((res) => {
    		commit('getShopData', res)
    		commit('displayPoints')
    		commit('setShopScore', res.data.shopDetail.recommendScore)
    		commit('getShopDetailIntro')
    	})
    }
```

*  这种方法一般是和页面直接引入action函数时连用
```js
    _this.getShopData().then()
```
###建议

1. vuex虽然使用起来特别方便，但是对于小型项目，组件划分不要太细
2. 提交状态尽量按照标准写法来提交，不要直接修改状态

date 2018.5.20 23:00

