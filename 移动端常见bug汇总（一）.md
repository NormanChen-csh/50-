# 移动端常见bug汇总（一）

1. 解决点击出现蓝色底框效果

    ```css
    -webkit-tap-highlight-color : rgba (255, 255, 255, 0) ;
    // i.e . Nexus5/Chrome and Kindle Fire HD 7 ''
    -webkit-tap-highlight-color : transparent ;
    ```

2. 禁止用户选择页面中的文字或者图片
    ```css
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    ```

3. 在iOS上，输入框默认有内部阴影，但无法使用 box-shadow 来清除，如果不需要阴影，可以这样关闭：

    ```css
    -webkit-appearance: none;
    ```

4. 禁止文本缩放

    ```css
    -webkit-text-size-adjust: 100%;
    ```

5. 禁止保存或拷贝图像,设置在需要禁止的图片类名上

    ```css
    -webkit-touch-callout: none;
    ```

6. 解决字体在移动端比例缩小后出现锯齿的问题

    ```css
    -webkit-font-smoothing: antialiased;
    ```

7. 设置input里面placeholder字体的大小

    ```css
    ::-webkit-input-placeholder: {
        font-size: 10pt;
    }
    ```
8. audio元素和video元素在ios和andriod中无法自动播放

    ```javascript
    $('html').one('touchstart',function(){
        audio.play()
    })
    ```

9. 手机拍照和上传图片，针对file类型增加不同的accept字段

    ```html
    <input type="file">的accept 属性
    <!-- 选择照片 -->
    <input type=file accept="image/*">
    <!-- 选择视频 -->
    <input type=file accept="video/*">
    ```

10. 开启硬件加速

    ```css
    -webkit-transform: translate3d(0, 0, 0);
    -moz-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    ```

11. 用户设置字号放大或者缩小导致页面布局错误

    ```css
    body
    {
        -webkit-text-size-adjust: 100% !important;
        text-size-adjust: 100% !important;
        -moz-text-size-adjust: 100% !important;
    }
    ```

12. 移动端去除type为number的箭头

    ```css
    input::-webkit-outer-spin-button,input::-webkit-inner-spin-button{
      -webkit-appearance: none !important;
      margin: 0;
    }
    ```