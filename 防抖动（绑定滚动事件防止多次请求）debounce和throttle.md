# 防抖动（绑定滚动事件防止多次请求）debounce和throttle

这里讲lodash提供的两个防抖动api

_.debounce 和 _.throttle的区别

总的来说throttle是debounce的一个修饰，两个api最终都会调用_.debounce

_.throttle 多给debouce传了一个maxWait选项，这个选项的意思是至少保证在每个maxWait时间内让func被调用一次


总结一下： _.deboucne()是在delay时间内才可以调用，操作停止后调用。_.throttle()是在maxWait或者说传入时间内至少调用一次。
可以说 _.throttle()就是设置了 leading=true,trailing=true 及maxWait的 _.debounce()

leading

一些应用场景：
	input 中 输入文字自动发送ajax请求 进行自动补全： debounce
    resize window 重新计算样式或者布局 debounce
    scroll 时更新样式，如随动效果 throttle

#### date 2018.5.23