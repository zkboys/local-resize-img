# local-resize-img
浏览器本地处理图片
## 安装：
bower install local-resize-img
或
git clone https://github.com/zkboys/local-resize-img.git
## 使用：
###单图上传：
```
<input id="single-img" type="file" name="file" value="">
$('#single-img').localResizeImg({
    quality: 0.75, // 图片压缩比例
    maxWidth: 260, //图片最大宽度
    maxHeight: 260,// 图片最大高度
    before: function (options) {//return false 可以阻止后续操作。
        // do something
    },
    success: function (data) {
        var base64 = data.base64; //可以作为img src属性值的数据
        var clearBase64 = data.clearBase64; //传给后台，后台用来生成图片的数据。
        var $img = $('<img src="" alt="">');
        $img.attr('src', base64);
        $('body').append($img);
        var $input = $('<input type="hidden" name="img-data" value="">');
        $input.val(clearBase64);
        $('body').append($input);
    }
});
```

###多图上传：
```
<input id="multiple-img" type="file" name="file" value="" multiple data-maxCount="5">
$('#multiple-img').localResizeImg({
    quality: 0.75, // 图片压缩比例
    maxWidth: 260, //图片最大宽度
    maxHeight: 260,// 图片最大高度
    before: function (options) {//return false 可以阻止后续操作。
        var maxCount = options.maxCount;
        if (options.files.length > maxCount) {
            if (maxCount <= 0) {
                alert('图片太多了，不能再传了！');
                return false;
            }
            alert('您最多能再选择' + maxCount + '张图片！');
            return false;
        }
    },
    success: function (data) {
        var base64 = data.base64; //可以作为img src属性值的数据
        var clearBase64 = data.clearBase64; //传给后台，后台用来生成图片的数据。
        var $img = $('<img src="" alt="">');
        $img.attr('src', base64);
        $('body').append($img);
        var $input = $('<input type="hidden" name="img-data" value="">');
        $input.val(clearBase64);
        $('body').append($input);
    }
});
```
