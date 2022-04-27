# my-html-note
## 多媒体与嵌入
### HTML中的图片
#### 最简单的图片
```javascript
<img src="images/dinosaur.jpg"
     alt="The head and torso of a dinosaur skeleton;
          it has a large head with long sharp teeth">
```
<img src="./pics/1.png" alt="这里使用了img标签插入了一张测试图片">

#### 备选文本和title
<em>实际上装饰性图片就不应该放在HTML文件里， CSS 背景图片才应该用于插入装饰图片</em>

图片的title不需要包含有意义的信息，这些信息应该放在alt属性里。

#### 宽高
图片的宽高可以使页面更快的加载，但是缺点是不正确的宽高会导致图片模糊或者扭曲。

#### \<figure\>为图片提供解释说明
有一个更好的做法是使用 HTML5 的 `<figure>` 和 `<figcaption>` 元素，它正是为此而被创造出来的：为图片提供一个语义容器

### 视频和音频
#### video
`source`标签提供源,
video的内容是视频的文字描述
```javascript
<video controls width="400" height="400"
       autoplay loop muted
       poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>你的浏览器不支持 HTML5 视频。可点击<a href="rabbit320.mp4">此链接</a>观看</p>
</video>
```

#### 音轨
用track标签链接 .vtt 文件，track 标签需放在 audio或 video 标签当中，同时需要放在所有 source>标签之后。使用 kind 属性来指明是哪一种类型，如 subtitles 、 captions 、 descriptions。然后，使用 srclang 来告诉浏览器你是用什么语言来编写的 subtitles。
```javascript
<video controls>
    <source src="example.mp4" type="video/mp4">
    <source src="example.webm" type="video/webm">
    <track kind="subtitles" src="subtitles_en.vtt" srclang="en">
</video>
```

### 嵌入技术
`<iframe>`用于嵌入其他网页，`embed`和`object`则允许您嵌入PDF，SVG，甚至Flash。

#### iframe
```javascript
<iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p> <a href="https://developer.mozilla.org/en-US/docs/Glossary">
    Fallback link for browsers that don't support iframes
  </a> </p>
</iframe>
```

#### embed
```javascript
<embed src="whoosh.swf" quality="medium"
       bgcolor="#ffffff" width="550" height="400"
       name="whoosh" align="middle" allowScriptAccess="sameDomain"
       allowFullScreen="false" type="application/x-shockwave-flash"
       pluginspage="http://www.macromedia.com/go/getflashplayer">
```

#### object
```javascript
<object data="mypdf.pdf" type="application/pdf"
        width="800" height="1200" typemustmatch>
  <p>You don't have a PDF plugin, but you can <a href="myfile.pdf">download the PDF file.</a></p>
</object>
```

#### svg
三种引用方法：1.img 2.svg 3.iframe

### 自适应图片
2种方式。1.切换图片 2.切换分辨率

#### 切换图片
```javascript
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

#### 切换分辨率
```javascript
<img srcset="elva-fairy-320w.jpg,
             elva-fairy-480w.jpg 1.5x,
             elva-fairy-640w.jpg 2x"
     src="elva-fairy-640w.jpg" alt="Elva dressed as a fairy">
```

#### picture标签
```javascript
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

#### 为什么不用js或者css来做这些？
当浏览器开始加载一个页面, 它会在主解析器开始加载和解析页面的 CSS 和 JavaScript 之前先下载 (预加载) 任意的图片。这是一个非常有用的技巧，平均下来减少了页面加载时间的20%。但是, 这对响应式图片一点帮助都没有, 所以需要类似 srcset的实现方法。因为你不能先加载好 <img> 元素后, 再用 JavaScript 检测可视窗口的宽度，如果觉得大小不合适，再动态地加载小的图片替换已经加载好的图片，这样的话, 原始的图像已经被加载了, 然后你又加载了小的图像, 这样的做法对于响应式图像的理念来说，是很糟糕的。
