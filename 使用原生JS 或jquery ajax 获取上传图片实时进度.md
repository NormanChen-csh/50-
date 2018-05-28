# 使用原生JS 或jquery ajax 获取上传图片实时进度

话不多说 直接上代码

## jquery 版

```
    $.ajax({
        url: 'URL',
        type: 'POST',
        data: fd,
        processData: false, //用来回避jquery对formdata的默认序列化，XMLHttpRequest会对其进行正确处理  
        contentType: false, //设为false才会获得正确的conten-Type  
        xhr: function() { //用以显示上传进度  
            var xhr = $.ajaxSettings.xhr();
            if (xhr.upload) {
                xhr.upload.addEventListener('progress', function(event) {
                    var percent = Math.floor(event.loaded / event.total * 100);
                    document.querySelector("#progress .progress-item").style.width = percent + "%";
                }, false);
            }
            return xhr
        },
        success: function(data) {

        }
    })
```

## 原生js版

```

var xhr = new XMLHttpRequest();
    xhr.open('POST', 'url');
    // 上传完成后的回调函数
    xhr.onreadystatechange = function() {
        if (xhr.status === 200) {　　
            console.log(xhr.responseText);
        } else {　
            console.log('上传出错');
        }
    };
    // 获取上传进度
    xhr.upload.onprogress = function(event) {
        console.log(event.loaded)
        console.log(event.total)
        if (event.lengthComputable) {
            var percent = Math.floor(event.loaded / event.total * 100);
            document.querySelector("#progress .progress-item").style.width = percent + "%";
            // 设置进度显示
            console.log(percent)
        }
    };
    xhr.send(fd);
```

## html 和相关进度条css

```
    <div id="progress">
        <div class="progress-item"></div>
    </div>
    #progress {
        height: 10px;
        width: 300px;
        border: 1px solid gold;
        position: relative;
        border-radius: 5px;
    }
    #progress .progress-item {
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background: chartreuse;
        border-radius: 5px;
        transition: width .3s linear;
    }
```

### 大字表示注意,网速快了 看到的进度条是一瞬间完成，打印的percent也都是100，如果要看比较明显的效果可以把控制台的模拟网速调成slow 3G,就能看到比较明显的效果。

#### date 2018.5.26
