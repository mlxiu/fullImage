# lightbox
div 内的图片，点击后放大查看。


# 使用第三方库

div 内点击图片放大的库比较多。这里使用的是 **Lightbox for Bootstrap**

> 官网： http://ashleydw.github.io/lightbox/  
> github: https://github.com/ashleydw/lightbox  
> cdn: http://www.bootcdn.cn/ekko-lightbox/

# 规则
使用别人的东西，就得遵守别人的规则。 Lightbox 的结构是这样的：

```
<a href="xxx.jpg" data-toggle="lightbox">
<img src="xxx.jpg" class="img-fluid">
</a>
```

这种是最简洁，单一的图片展示。如果想在展示图片的同时，还显示图片的 **title** 以及 底部说明。可以在 `a` 标签上额外加上 `data-title=` 和 `data-footer=` 。 如：

```
<a href="xxx.jpg" data-toggle="lightbox" data-title="如来神掌" data-footer="如果神掌可好看了。主演有张智霖和朱茵">
<img src="xxx.jpg" class="img-fluid">
</a>
```

如果想组成照片组。也就是图片放大后，可以左右切换图片查看，请在 `a` 标签中加入 `data-gallery=` 。 如：

```
<a href="xxx.jpg" data-toggle="lightbox" data-gallery="topics-gallery">
<img src="xxx.jpg" class="img-fluid">
</a>
```

# 创造规则

如果页面的内容产生不方便控制，也就是不能组成 `Lightbox` 想要的结构，可以通过 `js` 手动构造。通常，在页面正文中，有很多张图片。就是这种场景。比如写一篇文章，文章中会有一些插图。需要点击插图的时候，放大独立查看。这个时候，就可以构造了。如：

```
$(document).ready(function(){

  $('.panel-body img').each(function(){

      if($(this).hasClass('thumbnail'))
          return true;

      $(this).addClass('img-fluid');
      var originHtml = $(this).parent().html();
      var img = $(this).attr('src');
      var newhtml = '<a href="' + img + '" data-toggle="lightbox" data-gallery="topics-gallery">' + 
                     originHtml + '</a>';

      $(this).parent().empty().html(newhtml);
  });

  $(document).on('click', '[data-toggle="lightbox"]', function(event) {
                  event.preventDefault();
                  $(this).ekkoLightbox();
              });

});
```

如果是缩略图，小图，就不给它构造。

# 结尾多一句

做好以上这些，仅仅需要先引入css以及js就足够了。

```
<link href="https://cdn.bootcss.com/ekko-lightbox/5.3.0/ekko-lightbox.css" rel="stylesheet">
<script src="https://cdn.bootcss.com/ekko-lightbox/5.3.0/ekko-lightbox.js"></script>
```

体验可以查看： [https://www.rhbody.com/topics/8/a-beautiful-ancient-costume-and-martial-arts-drama](https://www.rhbody.com/topics/8/a-beautiful-ancient-costume-and-martial-arts-drama)
