## Demo

- [demo](https://htmlpreview.github.io/?https://github.com/zc95/enlargeImg/blob/master/index.html)

## 核心代码

### html部分

```html
<img class="enlargeImg" width="80" src="https://zc95.github.io/images/avatar.png"
title="点击查看大图" />
```

重点：

- img标签
- class="enlargeImg"
- 限制图片宽度或高度为"小图片"，width="80"
- src有值
- title="点击查看大图"

### css部分

```css
.enlargeImg_wrapper {
  display: none;
  position: fixed;
  z-index: 999;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  background-color: rgba(52, 52, 52, 0.8);
  background-size: 50%;
}

img:hover,
.enlargeImg_wrapper:hover {
  cursor: pointer;
}
```

重点：

- 半透明遮罩层 background-color: rgba(52, 52, 52, 0.8);
- 水平垂直居中 background-position: center;
- 放大后的图片大小 background-size: 50%;
- 如果受页面中别的定位元素的z-index影响，改z-index的值就行

### js部分

```javascript
$(function() {
  enlargeImg();
})
//查看大图
function enlargeImg() {
  $(".enlargeImg").click(function() {
    $(this).after("<div onclick='closeImg()' class='enlargeImg_wrapper'></div>");
    var imgSrc = $(this).attr('src');
    $(".enlargeImg_wrapper").css("background-image", "url(" + imgSrc + ")");
    $('.enlargeImg_wrapper').fadeIn(200);
  })
}
//关闭并移除图层
function closeImg() {
  $('.enlargeImg_wrapper').fadeOut(200).remove();
}
```

重点：

- 点击class为 `enlargeImg` 的图片时获取它的路径，var imgSrc = $(this).attr('src');
- 创建遮罩层，$(this).after("<div onclick='closeImg()' class='enlargeImg_wrapper'></div>");
- 赋值给 `enlargeImg_wrapper` ，$(".enlargeImg_wrapper").css("background-image", "url(" + imgSrc + ")");
- 关闭遮罩层时移除遮罩层，$('.enlargeImg_wrapper').fadeOut(200).remove();
