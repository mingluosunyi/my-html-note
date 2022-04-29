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


## 表格
### 表格基础
#### th
为了将表格的标题在视觉上和语义上都能被识别为标题，你可以使用 th 元素 ('th' 代表 'table header'). 用法和 td 是一样的，除了它表示为标题，不是普通的单元格以外。进入你的 HTML 文件, 将表格中应该是标题的 td 元素标记的内容，都改为用 th 元素标记。

表格标题也有额外的好处，随着 scope 属性 (我们将在下一篇文章中了解到)，这个属性允许你让表格变得更加无障碍，每个标题与相同行或列中的所有数据相关联。屏幕阅读设备能一次读出一列或一行的数据，这是非常有帮助的。

#### 允许单元格跨越多行和列
表格中的标题和单元格有 colspan 和 rowspan 属性，这两个属性可以帮助我们实现这些效果。

#### 为表格中的列提供共同的样式
 col  元素被规定包含在  colgroup 容器中，而 colgroup 就在 table 标签的下方。
```javascript
<table>
  <colgroup>
    <col>
    <col style="background-color: yellow">
  </colgroup>
  <tr>
    <th>Data 1</th>
    <th>Data 2</th>
  </tr>
  <tr>
    <td>Calcutta</td>
    <td>Orange</td>
  </tr>
  <tr>
    <td>Robots</td>
    <td>Jazz</td>
  </tr>
</table>  
```
对于第一列，我们没有采取任何样式，但是我们仍然需要添加一个空的 col 元素，如果不这样做，那么我们的样式就会应用到第一列上，这和我们预想的不一样。

#### 使用caption为表格添加标题
标题就放在 table 标签的下面。

#### 使用thead，tbody和tfoot
<em>tbody在html的顺序不影响渲染的结果。</em>

#### 使用scope属性
本篇文章的一个新话题是 scope 属性，可以添加在 *th* 元素中，表明这是列标题还是行标题
```javascript
<tr>
  <th scope="row">Haircut</th>
  <td>Hairdresser</td>
  <td>12/09</td>
  <td>Great idea</td>
  <td>30</td>
</tr>
```
scope 还有两个可选的值 ：colgroup 和 rowgroup
这几个单元格都应该被标记为 ( th )，但是 "Clothes" 是一个位于顶部且定义了其他三个子标题的标题。 因此 "Clothes" 应该有一个 scope="colgroup"属性，而另外三个子标题应该有 scope="col"属性。

## html基础
### 网站框架
![frame](./pics/截屏2022-04-29%20上午10.41.49.png)

### 高级文字排版
#### 描述列表
dl,dt,dd
#### 引用
引用分为块引用和行内引用
分别是blockquote和q标签，这两个标签都有cite属性。
如果想要显示cite，需要加上a标签在其中嵌套cite标签
```javascript
<p>你好！欢迎访问我的激励网页！<a href="http://www.brainyquote.com/quotes/authors/c/confucius.html"><cite>孔子</cite></a>曰：</p>
<blockquote cite="https://zh.wikipedia.org/zh-hans/孔子">
  <p>譬如为山，未成一篑，止，吾止也。譬如平地，虽覆一篑，进，吾往也。</p>
</blockquote>
<p>要保持乐观，<q cite="http://www.affirmationsforpositivethinking.com/">不要说泄气的话</q>。（源自 <a href="http://www.affirmationsforpositivethinking.com/"><cite>Affirmations for Positive Thinking</cite></a>。）</p>
```

#### 缩略语
abbr 和title属性用来表示一个缩略语和他的解释
```javascript
<p><abbr title="美国国家航空航天局（National Aeronautics and Space Administration）">NASA</abbr> 做了一些动人心弦的事情。</p>
```
#### 联系方式
address

#### 上下标
sub，sup

#### 计算机代码
![code](./pics/截屏2022-04-29%20上午11.20.41.png)

#### 日期
将时间和日期标记为可供机器识别的格式
```javascript
<time datetime="2016-01-20">20 January 2016</time>
```

### 文本基础
列表，strong，em。
在没有更好办法的情况下b、i 或 u 来表达传统上的粗体、斜体或下划线。

## 表单
TODO