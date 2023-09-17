# docsify的配置+全插件列表-腾讯云开发者社区-腾讯云
docsify的配置+全插件列表
----------------

原创

![](https://ask.qcloudimg.com/http-save/yehe-7689800/31348300d1450944b19358742377b053.jpeg)

星橙

已关注

发布于 2022-11-28 09:34:30

4.2K2

发布于 2022-11-28 09:34:30

举报

本篇文章来自好友肥子哥，原文连接：[https://xhhdd.cc/index.php/archives/80/](/developer/tools/blog-entry?target=https%3A%2F%2Fxhhdd.cc%2Findex.php%2Farchives%2F80%2F)

引子
--

有天球球在群里说handsome作者的文档网站还挺好看的，不知道用什么模板做的。

有个大佬立马告诉我们是用的docsify。

然后球球就去踩坑了，去研究怎么安装。

[docsify的官方文档](/developer/tools/blog-entry?target=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2F)

![](https://ask.qcloudimg.com/http-save/7689800/daff0c9d153c27b534a9e85bb60bb9f6.png)

![](https://ask.qcloudimg.com/http-save/7689800/afe72e78d48d33b72a6a483c43306e7b.png)

有一说一，是还挺好看的。里面的内页也是简洁明了，是我喜欢的类型。

它专门用来渲染md文件，和适合用`markdown`来写作的人，用来做文档站什么的。

![](https://ask.qcloudimg.com/http-save/7689800/69dea9ddebac990d40eaa29cd3b672e6.png)

安装流程
----

虽然说这样我也算是打开了，但是具体怎么配置我还一概不知，接下来我就研究了文档，然后观察了球球发给我的文件夹。

### 结构

![](https://ask.qcloudimg.com/http-save/7689800/3a37ecc9c03a489bfe07721b1cc8d187.png)

[https](/developer/tools/blog-entry?target=https%3A%2F%2Fcdntc.xhhdd.cc%2F2021%2F04%2F02%2F16172931195282.png)

网站的根目录下很多文件，乍一看非常的复杂，但是实际上我们可以简单的分成三个板块。

1.  `index.html`是最核心的一个文件，它里面加载了docsify的css、js，而且像网站的名字、ico、等基本的信息，还有插件的配置参数都是在这个文件当中。
2.  `docs文件夹`里面装的都是md文件，网站会渲染这些用markdown语法写成的文章在前台展示出来。
3.  `其他的md文件`是与`index.html`衔接的有联系的一些文件，比如说侧边栏的目录、页脚文件等。

那知道了结构之后，我们首先要对`index.html`文件进行一个设置。

本小白到了这一次才对html语法有些微了解，所以准备从0开始自己完整的写好这个文件。

### 写html文件

我知道最大的标签是`<html>`，它包裹着里面的内容。然后最开始是`<head>`的标签，是头的意思吗？所以写在最开头哈哈哈哈~

```
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="renderer" content="webkit">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <!-- 网站描述+关键字+作者 -->
    <meta name="description" content="邓邓的个人wiki站，收集、整理、提炼所学的知识">
    <meta name="keywords" content="wiki,docsify,音乐爱好者">
    <meta name="author" content="xhhdd">
    <title>邓邓的零食橱</title>
    <!-- docsify的主题样式 -->
    <link rel="stylesheet" href="//vox.cab/npm/docsify/lib/themes/vue.css">
    <!-- 侧边栏插件的样式 -->
    <link rel="stylesheet" href="//vox.cab/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
</head>
```

复制

好了以上是我写的内容

*   `<meta charset="UTF-8">`应该就是声明一下字符编码
*   `http-equiv`不是很了解，说是http的请求头，我顺便在下面加了一行，是从handsome那里加过来的，据说是针对国内浏览器的优化
*   `viewport`应该是搞那个什么移动设备适配的，我还去查了哪个参数是对应锁定宽度，哪个参数是不允许放大缩小之类的
*   然后那些网站的描述不知道是不是这样写的，我也依样画葫芦...
*   最底下的就是一些样式文件，我也是直接复制粘贴，要什么就粘贴什么

好了之后，接下来就是`<body>`里面的内容了

```
<body>
    <!-- 定义加载时的显示 -->
    <div id="app">很快！等我一下！</div>
    <script>
        window.$docsify = {
            //通用设置
            // -----------------------------------------------------
            // 加载自定义导航栏,需要目录下有_navbar.md文件
            loadNavbar: true,
    </script>
    <!-- docsify的js依赖 -->
    <script src="//vox.cab/npm/docsify/lib/docsify.min.js"></script>
```

复制

这个看起来好像有点复杂。

*   首先最上面`<div id="app">很快！等我一下！</div>`这个是指定加载页面等待时显示的内容
*   然后中间`<script>`标签里面的是`window.$docsify` 的配置参数，这个非常的重要，一些基本的配置项目都是在这里实现的，我们在这里照着[文档](/developer/tools/blog-entry?target=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2Fconfiguration)一个一个的选择自己需要的参数填上去。
*   最后是加载js的地方，过会装插件的时候会用的上。

这里要特别说一下，我在看文档的时候，上面是这么写的

![](https://ask.qcloudimg.com/http-save/7689800/1c745d6e49af74d97c4c3c85c4c0bc7b.png)

我以为是下面这种写法

```
window.$docsify = {
  maxLevel: 4,
};
window.$docsify = {
  loadNavbar: true,
  loadNavbar: 'nav.md',
};
```

复制

其实不用这么复杂，`window.$docsify`只需要写一个就可以了。

```
window.$docsify = {
  maxLevel: 4,
  loadNavbar: true,
  loadNavbar: 'nav.md',
};
```

复制

在这里我吃过无数次亏的就是

逗号！逗号！

要不就是最后一个写了逗号，要不就是中间没写逗号

真的是气死我了

当然各位大佬估计不会犯本小白这样的错误...

所以到这里呢，我们的html文件基本上就写好了，在写的过程中就会发现，有些配置参数是需要别的文件支持的。比如说开启侧边栏，就需要在根目录下建立一个`_sidebar.md`文件，然后在里面写好内容。也就是我们刚才上文中所说的第三类文件。

* * *

接下来，我们来看一下插件怎么安装

![](https://ask.qcloudimg.com/http-save/7689800/4b5c61210e830cb151dea9c3834eb990.png)

我们大部分的插件安装都是做两件事情

1.  加载js：就是把它给你的这一行代码，复制粘贴到`<body>`标签的最下方
2.  添加配置参数：就是把这些参数复制粘贴`<body>`下的`window.$docsify`中

**简而言之！都是在`index.html`中进行操作！而且就是复制粘贴！**

那根据文档说的，我们就会这么来写

```
<body>
    <!-- 定义加载时的显示 -->
    <div id="app">很快！等我一下！</div>
    <script>
        window.$docsify = {
          //字数插件
          count:{
              countable:true,
              fontsize:'0.9em',
              color:'rgb(90,90,90)',
              language:'chinese'
              }
          }
        }
    </script>
    <!-- docsify的js依赖 -->
    <script src="//vox.cab/npm/docsify/lib/docsify.min.js"></script>
    <!-- 字数插件 -->
    <script src="https://vox.cab/npm/docsify-count@latest/dist/countable.min.js"></script>
```

复制

好了，大概就是这个意思。

下文中我附上了docsify所有插件的链接，和我能看懂的插件的详细安装方法，可以去参考一下。

* * *

**补充一下侧边栏文件`_sidebar.md`的写法**

我们新建一个`_sidebar.md`之后

*   在里面写上文字，都会在侧边以文字的形式展示出来，能正常的解析一些md语法与html的语法（如加粗，指定颜色等）
*   如果想要链接到md文档，跟md里图片的语法非常相像，方框里是目录的名称，括号里是md文件的地址。此时侧边栏的会出现`docs`，并且点击即可查看渲染好的`docs.md`

```
- [docs](docs/docs.md)
```

复制

*   如果想要多级目录，请参照底下`侧边栏插件`的详细用法

* * *

以上，`index.html`文件就是这些内容，接下来发一下我写的，可以复制粘贴到网站根目录看看效果。

```
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="renderer" content="webkit">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <!-- 网站描述+关键字+作者 -->
    <meta name="description" content="邓邓的个人wiki站，收集、整理、提炼所学的知识">
    <meta name="keywords" content="wiki,docsify,音乐爱好者">
    <meta name="author" content="xhhdd">
    <title>邓邓的零食橱</title>
    
    <!-- docsify的主题样式 -->
    <link rel="stylesheet" href="//vox.cab/npm/docsify/lib/themes/vue.css">
    <!-- 侧边栏插件的样式 -->
    <link rel="stylesheet" href="//vox.cab/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
</head>
<body>
    <!-- 定义加载时的显示 -->
    <div id="app">很快！等我一下！</div>
    <script>
        window.$docsify = {
            //通用设置
            // -----------------------------------------------------
            // 加载自定义导航栏,需要目录下有_navbar.md文件
            loadNavbar: true,
            // 开启侧边栏，需要目录下有_sidebar.md文件
            loadSidebar: true,
            // 读取md文件中最大几级目录
            subMaxLevel: 2,
            // 切换页面后跳回页面顶部
            auto2top: true,
            // 指定开始页
            homepage: '_home.md',
            //开启封面页，需要目录下有_coverpage.md文件
            coverpage: true,
            // 侧边栏左侧的logo
            logo: '',
            // 侧边栏顶部的标题
            name: '邓邓的零食橱',
            // 点击标题后的跳转地址
            nameLink: '/',
            // 禁用emoji
            noEmoji: true,
            // 移动设备合并导航栏到侧边栏
            mergeNavbar: true,
            // 加载_404.md
            notFoundPage: true,
            // 滚动到锚点是与顶部的距离
            topMargin: 90,
            //插件设置
            // -----------------------------------------------------
            // 搜索配置
            search: {
                maxAge: 86400000,
                paths: 'auto',
                placeholder: '搜索',
                noData: '找不到结果',
                depth: 4,
                hideOtherSidebarContent: false,
                namespace: '邓邓的零食橱'
            },
            // 字数插件
            count:{
                countable: true,
                position: 'top',
                margin: '10px',
                float: 'right',
                fontsize:'0.9em',
                color:'rgb(90,90,90)',
                language:'chinese',
                localization: {
                    words: "",
                    minute: ""
                },
                isExpected: true
            },
            // 分页导航插件
            pagination: {
                previousText: '上一卷',
                nextText: '下一卷',
                crossChapter: true,
                crossChapterText: true
            },
            // 文本高亮
            'flexible-alerts': {
                style: 'flat',
                note: {
                    label: "信息"
                },
                tip: {
                    label: "提示"
                },
                warning: {
                    label: "注意"
                },
                attention: {
                    label: "切记"
                }
            },
            sidebarDisplayLevel: 2,
            // 页脚信息插件
            loadFooter: true,
            loadFooter: '_footer.md'
        };
    </script>
    <!-- docsify的js依赖 -->
    <script src="//vox.cab/npm/docsify/lib/docsify.min.js"></script>
    <!-- 搜索 -->
    <script src="//vox.cab/npm/docsify/lib/plugins/search.min.js"></script>
    <!-- 图片放大缩小支持 -->
    <script src="//vox.cab/npm/docsify/lib/plugins/zoom-image.min.js"></script>
    <!-- 字数插件 -->
    <script src="https://vox.cab/npm/docsify-count@latest/dist/countable.min.js"></script>
    <!-- 分页导航 -->
    <script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
    <!-- 文本高亮 -->
    <script src="https://unpkg.com/docsify-plugin-flexible-alerts"></script>
    <!-- 侧边栏扩展与折叠 -->
    <script src="//vox.cab/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
    <!-- 页脚信息 -->
    <script src="//vox.cab/npm/@alertbox/docsify-footer/dist/docsify-footer.min.js"></script>
</body>
</html>
```

复制

docsify的插件
----------

docsiff有很多插件，但是没有中文版的，我尽我所能把我会的去试了一下，希望能帮到大家。

![](https://ask.qcloudimg.com/http-save/7689800/a0f9dadfc3a57e469636432db8096e9e.png)

我们上文说到这些插件的安装方法都是比较统一的

1.  把js代码复制粘贴进`index.html`这个文件
2.  在`index.html`中的window.$docsify 下填写好配置参数

### 分享插件[docsify-share](/developer/tools/blog-entry?target=https%3A%2F%2Fcoroo.github.io%2Fdocsify-share%2F%23%2F)

A Plugin to add share button in your docsify. @coroo.

这是一个分享的插件，安装之后就会在页面的右下角出现一个分享图案，目前支持以下几个平台

![](https://ask.qcloudimg.com/http-save/7689800/1cd4aeb65169d4c57b2ae90adcf1822d.png)

首先是js代码

```
<script src="//unpkg.com/docsify-share/build/index.min.js"></script>
```

复制

然后是配置参数

```
<script>    window.$docsify = {        share: {            reddit: true,            linkedin: true,            facebook: true,            twitter: true,            whatsapp: true,            telegram: true,        }    };</script>
```

复制

再具体一点去它的官方页面看吧~

不过我可能是没学会，那个图标是出现了，也可以跳转到对应的软件，可就是没有下文，不知道怎么分享出去了~

### 字数插件[docsify-count](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2F827652549%2Fdocsify-count%2F)

Add word count for markdown files of docsify.(添加字数统计)@827652549.

> 这个插件与`阅读进度条`插件不兼容

这是一个字数统计插件，它提供了统计中文汉字和英文单词的功能，并且排除了一些markdown语法的特殊字符例如*、-等

![](https://ask.qcloudimg.com/http-save/7689800/982479a3283d6f72a35746cbf6889251.png)

首先是添加js

```
<script src="//unpkg.com/docsify-count/dist/countable.min.js"></script>or<script src="https://vox.cab/npm/docsify-count@latest/dist/countable.min.js"></script>
```

复制

然后是配置参数

```
window.$docsify = {  count:{    countable: true,    position: 'top',    margin: '10px',    float: 'right',    fontsize:'0.9em',    color:'rgb(90,90,90)',    language:'chinese',    localization: {      words: "",      minute: ""    },    isExpected: true  }}
```

复制

按理来说在`words`与`minute`里面是可以填上自己自定义的字的，不知道为什么操作不了...

### [docsify-rtl](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fckoliber%2Fdocsify-rtl)

Add rtl and bidi support to docsify @koliberr136a1.

这个没看懂，不知道干嘛的。描述上说是

`It will automatically changes the body, side, bdo directions`

### 加载远程文档[docsify-remote-markdown](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FJerryC8080%2Fdocsify-remote-markdown)

Load markdown docs from remote. @JerryC.

不太清楚这个功能有啥用，加载一个远程的md文件。那我为什么不直接放在[服务器](https://cloud.tencent.com/act/pro/promotion-cvm?from_column=20065&from=20065)呢？

反正我的话不是很用得上。

### 分章节按钮[docsify-pagination](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fimyelo%2Fdocsify-pagination)

Pagination for docsify @imyelo.

这是一个分章节的插件，它会在文章的底部提供一个按钮跳转到下一个（或上一个）MD文件。

文件的排序是根据左侧的侧边栏来的。

其中`下一章节`这几个字也可以进行自定义，变成`下一卷`、`下一页`之类的。

![](https://ask.qcloudimg.com/http-save/7689800/c0131ae18f3e6024c56f492651fad757.png)

首先是加载js

```
<script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

复制

然后是配置参数

```
window.$docsify = {  // ...  pagination: {    previousText: '上一章节',    nextText: '下一章节',    crossChapter: true,    crossChapterText: true,  },}
```

复制

这个能够配置的比较少，看一眼基本上懂了。

### 绘图[docsify-plantuml](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fimyelo%2Fdocsify-plantuml)

PlantUML for docsify @imyelo.

plantuml应该是比较熟悉了，是一个做流程图的插件。

![](https://ask.qcloudimg.com/http-save/7689800/9c5851ca80e2461d6492e631aa90351b.png)

填入代码

![](https://ask.qcloudimg.com/http-save/7689800/abc0b76cdafbf04da3c5cc1357f9c6d7.png)

那就会出来以上这个效果

不过我基本上用不到这玩意~~

### 绘图[docsify-puml](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Findieatom%2Fdocsify-puml)

Docsify plugin to parse PlantUML content @indieatom.

跟上面那个一样，也是一个做流程图的插件

### 代码复制框[docsify-copy-code](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fjperasmus%2Fdocsify-copy-code)

A docsify plugin that copies Markdown code block to your clipboard @jperasmus.

这是一个代码的复制弹框，说实话真的很朴素。

![](https://ask.qcloudimg.com/http-save/7689800/90bcfc0bd2853e2e55cabf3ec0fe81d0.png)

按下复制按钮之后，会滑动出一个`复制成功`的字，不过不是很好截图就没有弄了，主要真的不是很好看...

不过这个插件有一个比较特别的地方，就是会支持多语音的那种文档，可以统一在配置文档那里调整。

> 看完所有的插件回来，我发现只有这一个代码复制插件...

### vue[docsify-demo-box-vue](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fnjleonzhang%2Fdocsify-demo-box-vue)

Write Vue demo in docsify with instant preview and jsfiddle integration @njleonzhang.

不太能看懂是什么意思~应该是那种页面上的代码模拟器？

### react[docsify-demo-box-react](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fnjleonzhang%2Fdocsify-demo-box-react)

Write React jsx demo in docsify with instant preview and jsfiddle integration @njleonzhang.

跟上一个是同一个作者，好像插件的性质是一样的

### [docsify-edit-on-github](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fnjleonzhang%2Fdocsify-edit-on-github)

Add Edit on GitHub button on every pages @njleonzhang.

这个插件应该是针对托管在github上的网站，可以进行一个快速的编辑。

### 标签卡[docsify-tabs](/developer/tools/blog-entry?target=https%3A%2F%2Fjhildenbiddle.github.io%2Fdocsify-tabs%2F%23%2F)

A docsify plugin for displaying tabbed content from markdown @jhildenbiddle.

这个是大致的效果

![](https://ask.qcloudimg.com/http-save/7689800/f26069e47bebe111b8cdb4d35592a32b.png)

```
<!-- tabs:start -->...<!-- tabs:end -->
```

复制

> 语法上来看的话不是很复杂，本来我是想试一下的。但是现在遇到的问题就是从handsome转过来的时候，很多这样的语法不适配。我在想万一以后我还要换的话怎么办...那就更麻烦了，最好还是通用会比较好。

### KATEX[docsify-katex](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fupupming%2Fdocsify-katex)

A docsify plugin for rendering LaTex math equations @upupming.

katex是一个数学公式引擎，懂得都懂，我直接放弃。

### 插入PDF[docsify-pdf-embed](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Flazypanda10117%2Fdocsify-pdf-embed)

A docsify plugin for embedding PDF on any page @lazypanda10117.

这个插件就是用来插入PDF的，我也是用不上~

### 文本高亮[docsify-plugin-flexible-alerts](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Ffzankl%2Fdocsify-plugin-flexible-alerts)

A docsify plugin to convert blockquotes into beautiful and configurable alerts using preconfigured or own styles and alert types. @fzankl.

这个其实跟handsome里面那个高亮提示文本差不多一个意思。

![](https://ask.qcloudimg.com/http-save/7689800/f1206a375aec62ef15651473c7db0397.png)

![](https://ask.qcloudimg.com/http-save/7689800/e1225755911c12d4eed31a60912d5107.png)

这个插件一共是支持四种高亮形式，分别是`note`、`tip`、`WARNING`、`ATTENTION`，用蓝绿黄红来进行一个区分。（handsome也是这样~这是一个通用的范式吗？)

然后看上图，左右两边分别是不同的样式，左边的框框是空的，右边的框是填充了颜色的。

> 本来我之前想说，像这种特别语法，最好还是不要用，不然以后万一要换平台的话真的很麻烦。但是.....但是这个真的太好看了。

首先是加载js

```
<script src="https://unpkg.com/docsify-plugin-flexible-alerts"></script>
```

复制

如果不配置参数的话，那么就是上图左边的样式。如果需要右边的样式的话，则需要

```
<script>  window.$docsify = {    'flexible-alerts': {      style: 'flat'    }  };</script>
```

复制

也就是说styl默认是`call out`上图左边的样式，指定为`flat`即为右边那种颜色填充的样式。

接下来怎么使用呢？

在文档中输入

```
> [!tip]> 填写你要的内容
```

复制

下图就是实际效果

![](https://ask.qcloudimg.com/http-save/7689800/845ac0723c1a8ef583cefc9e6d018150.png)

因为我刚才指定了style为`flat`，所以全局都是这种默认用颜色填充的框

如果想这一条文本单独换成`callout`也是可以的，只需要

```
> [!tip|style:callout]> 填写你要的内容
```

复制

则会变成下图的效果

![](https://ask.qcloudimg.com/http-save/7689800/2f22bf800e5f0a6dea5d1c6a7db166bc.png)

以上，简单总结一下。这个插件拥有`两种显示样式`、`四种高亮文本框`，可行进行全局设置样式或单个文本指定样式。

* * *

基本的使用就到这里了~接下来是进阶的用法

*   自定义高亮标题
*   自定义高亮文本框

首先是自定义高亮标题的配置参数

```
<script>  window.$docsify = {    'flexible-alerts': {      note: {        label: "测试"      }    }  };</script>
```

复制

那么就会显示

![](https://ask.qcloudimg.com/http-save/7689800/1771257b7d34fb017443861d16595fe7.png)

如果想要单独指定高亮的标题也是可以的，这样也会出现上图的效果。

```
> [!note|style:callout|label:测试]> 测试自定义
```

复制

*   然后是关于自定义高亮文本的样式，可以更换左上角的小图标、以及颜色自定义标题什么的 但是有点复杂，可以去作者的页面看一下~

### [docsify-pdf-converter](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fmeff34%2Fdocsify-to-pdf-converter)

Create PDF files based on your docsify project @meff34.

这个是啥？PDF转换？

我看到一开始的npm命令我就头大...

### 评论系统[docsify-commento](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fndom91%2Fdocsify-commento)

Append commento section to the bottom of every page @ndom91.

commento 是一个轻量级的评论系统，这个插件把commento嵌入到页面中。

安装反正我是看不懂了，直接放弃~

### gif插件[docsify-gifcontrol](/developer/tools/blog-entry?target=https%3A%2F%2Fgbodigital.github.io%2Fdocsify-gifcontrol%2F%23%2F)

A docsify plugin that adds customizable player controls to GIFs. @adambergman from @gbodigital.

我就喜欢这种简单易懂的插件，它可以控制gif的播放形式。比如点击播放，或者是鼠标放到图片上才进行播放。

不过我没有放gif图的需求~就没有去弄了

### [docsify-example-panels](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FVagnerDomingues%2Fdocsify-example-panels)

A plugin for rendering slate alike right example panels.

这个插件是令我百思不得其解，不知道它的功能是什么...翻译了也看不懂

但是感觉它的实例网站又很不一样？是左右两栏？

### [docsify-glossary](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FTheGreenToaster%2Fdocsify-glossary)

A plugin to create a simple glossary for common terms.

glossary是词汇表的意思？我看到用法就是说要建立一个文件，然后使用的时候要用`####`四级标题包围...

好吧，完全没懂。

### 目录跳转[docsify-toc](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fmrpotatoes%2Fdocsify-toc)

Add a Table of Contents to your site. @mrpotatoes.

这个插件其实蛮实用的，设置以后会在右边出现一个目录跳转，点击以后可以跳转到对应的标题。

![](https://ask.qcloudimg.com/http-save/7689800/bcceda7654f0ae13bd149f05bea276aa.png)

也是先加载js

```
<script src="https://unpkg.com/docsify-toc@1.0.0/dist/toc.js"></script>
```

复制

再加载stylesheet，一下这行代码放在`head`标签里

```
<link rel="stylesheet" href="https://unpkg.com/docsify-toc@1.0.0/dist/toc.css">
```

复制

最后是配置参数

```
window.$docsify = {  toc: {    scope: '.markdown-section',    headings: 'h1, h2, h3, h4, h5, h6',    title: 'Table of Contents',  },}
```

复制

从上面也能看出来，标题的层级是可以自选的，比如只加载`h2、h3`

> 最后就是关于这个插件出现的时机，因为在桌面端的话，左侧已经是有目录了，右边这个就显得比较多余。但是在手机浏览器上出现的话其实还不错。
> 
> ![](https://ask.qcloudimg.com/http-save/7689800/a411748003f530d2f8d30c7dae8deda3.jpg)

### fontawesome ico[docsify-fontawesome](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Ferickjx%2Fdocsify-fontawesome)

Add FontAwesome to documentation by tokens.

好了，FontAwesome算是比较熟悉的了，之前打过很多交道了。

这个正好可以配合上面那个文本高亮的插件一起使用，或者是别的目录什么地方，去插入图标这样子。

### [docsify-footer-enh](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Ferickjx%2Fdocsify-footer-enh)

Footer Enhancement plugin.

很尴尬，没看懂讲的啥~

### Mustache[docsify-mustache](/developer/tools/blog-entry?target=https%3A%2F%2Fdocsify-mustache.github.io%2F%23%2F)

A docsify plugin that allow preprocessing markdown documents with Mustache template engine.

Mustache模板嘛，好吧，我不懂。

### bitbucket[docsify-bitbucket](/developer/tools/blog-entry?target=https%3A%2F%2Fdocsify-bitbucket.github.io%2F%23%2F)

A docsify plugin that help using docsify with Bitbucket Server and Bitbucket Cloud.

bitbucket好像也是github那种网站？

### 两列布局[docsify-slides](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fshawntabrizi%2Fdocsify-slides)

A plugin for creating slideshow-like pages.

slides是ppt的意思？但这是一个两列布局的插件。

配置挺简单的。

首先是加载js

```
<script src="//unpkg.com/docsify-slides/dist/docsify-slides.min.js"></script>
```

复制

然后不需要配置参数，只需要把下面的命令放到md文件就可以了

```
<!-- slide:break -->or<!-- slide:break-# -->
```

复制

比如我选择放到文章的三分之一处，则文章的前三分之一会出现在网站的左边，剩下的三分之二会出现在网站的右边。

又比如说我放到文档的中间

![](https://ask.qcloudimg.com/http-save/7689800/28309aade0f771775212b2f9ded392d1.png)

则会出现下图的效果

![](https://ask.qcloudimg.com/http-save/7689800/a48d0771d6e9f3da2a4cf56d9abc0bf0.png)

当然我也可以填写

```
<!-- slide:break-30 -->
```

复制

![](https://ask.qcloudimg.com/http-save/7689800/83d04c6937100acf8e79be2ae8443c75.png)

则会变成上图那样。

> 这个插件我好像没有太多的用处，不过说实话，有时候是觉得整个内容横着排列有点满，但是有些内容直接竖着排也会比较好看。 还有就是上面两张图的实际上标题都没有对齐，显得比较难看。原作者说他用了什么空白标签对齐了高度，反正我是没搞明白是怎么回事...
> 
> ![](https://ask.qcloudimg.com/http-save/7689800/c3a505baa226fddb650f7570a3bee33b.png)

### phaser[docsify-Phaser](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fluisalvesmartins%2FdocsifyPhaser)

Enable Phaser code inside a docsify page.

这个插件说能让Phaser代码在网站上跑起来，Phaser是搞游戏的，好像是~

### 更新记录[docsify-changelog-plugin](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FPlugin-contrib%2Fdocsify-plugin%2Ftree%2Fmaster%2Fpackages%2Fdocsify-changelog-plugin)

Integrates your changelog in a sweet panel.

这个是搞那种更新记录的吧

![](https://ask.qcloudimg.com/http-save/7689800/465eabd468c35b148257d9316e66df1c.png)

不过我用不上~

### 横幅插件[docsify-top-bannner-plugin](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FPlugin-contrib%2Fdocsify-plugin%2Ftree%2Fmaster%2Fpackages%2Fdocsify-top-banner-plugin)

Add a simple and sweet banner at the top in order to announce something.

这是一个横幅插件~可以用来做一个更新通知啥的~

![](https://ask.qcloudimg.com/http-save/7689800/9ab4016748c9b8b5af76e048dccb4973.png)

然后能够自定义很多参数~

### 暗黑模式[docsify-dark-mode](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FPlugin-contrib%2Fdocsify-plugin%2Ftree%2Fmaster%2Fpackages%2Fdocsify-dark-mode)

Add dark mode support in your docsify site.

暗黑模式，可是我一直不是很喜欢，感觉看的不是很清楚。

### 评论[docsify-valine](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fdaidi%2Fdocsify-valine%2F)

A docsify plugin that allows you to use a fast, simple & powerful comment system valine on your docsify pages.

一个评论系统~

### emoji[docsify-twemoji](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FTaQini%2Fdocsify-twemoji)emoji

A plugin that allow parsing all emoji in style of twemoji for docsify.(推特 emoji)

引入推特版本的emoji，据说还比较全~

可以看看中文版的[安装指引](/developer/tools/blog-entry?target=http%3A%2F%2Ftaqini.space%2F2020%2F04%2F08%2Fdocsify-plugins%2F%23%25E6%258F%2592%25E4%25BB%25B6%25E6%258E%25A5%25E5%258F%25A3)

### 评论系统[docsify-livere](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FTaQini%2Fdocsify-livere)

An easy-installing plugin for awesome comment system LiveRe on your docs.(来必力评论插件)

跟上一个插件一样，有个中文版本的[安装指引](/developer/tools/blog-entry?target=http%3A%2F%2Ftaqini.space%2F2020%2F04%2F08%2Fdocsify-plugins%2F%23%25E6%258F%2592%25E4%25BB%25B6%25E6%258E%25A5%25E5%258F%25A3)

这个插件说是支持国内常见的登录方式：QQ、微信、github、百度、微博等等

### 选择框[docsify-select](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fjthegedus%2Fdocsify-select)

Variably render content with select menus in markdown.

这是一款选择框工具，可以生成的选择框。选择不同的选项能展示不同的内容~

而且跟之前的`tab`插件好像是兼容的还是有什么独特的联系~

不过我想这个用的时候又是新的语法...我就不去折腾了

### 绘图[docsify-mermaid](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FLeward%2Fmermaid-docsify)

A plugin to render mermaid diagrams in docsify.

这好像是markdown的绘图插件，总之也是生成各种流程图之类的东西。

### [docsify-plugin-carbon](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fwaruqi%2Fdocsify-plugin-carbon)

A plugin to make you easy to add Carbon Ads to docsify.

不懂跳过

### [docsify-pangu](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fsy-records%2Fdocsify-pangu)

A docsify plugin for Chinese and English, numbers, symbols and automatically add spaces between. @sy-records.

> 一个 docsify 插件：使用 pangu.js 给网页上的中文和英文、数字、符号之间添加空格。

不明白为什么要这样，应该是我还没有这么高的需求

### 支持gtlf[docsify-gtlfexplorer](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FX-Ryl669%2Fdocsify-gltfexplorer)

A plugin to embed a manipulable 3D model in your documentation.

在网页上加载3D对象，gtlf格式的。

### 封面图标[docsify-corner](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FKoooooo-7%2Fdocsify-corner)

A enhancement plugin for more repo widgets in top right corner, such as Gitlab. @Koooooo-7

这个插件可以让封面的右上角出现一个小图标，并且进行网址跳转。

本来docsify会让这里出现github的小图标，然后这个插件会对其进行一个替换与自定义。

不过我失败了，应该是以前属于docsify本身的配置没有弄好。

操作还是蛮简单的，感兴趣的可以去看看。

### [docsify-autoHeader](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fmarkbattistella%2Fdocsify-autoHeaders)

Turn your markdown into a cascading numbered document. Great for large documentation without manually numbering all the headings. @markbattistella

自动给标题排序？有点没有弄明白是怎样的，照着设置了一下，但操作失败了。

### 侧边栏页脚[docsify-sidebarFooter](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fmarkbattistella%2Fdocsify-sidebarFooter)

Add some links to the base of your sidebar - copyright year, company, Privacy Policy, Terms of Service.

这个插件能够在侧边栏底部生成一些基本的信息，比如说什么版权之类的

![](https://ask.qcloudimg.com/http-save/7689800/93a890597e16acbfe2da580f636d1f15.png)

但是这个插件安装过程比较的坑~

首先是加载js

```
<!-- unpkg.com --><script src="https://unpkg.com/@markbattistella/docsify-sidebarfooter@latest"></script><!-- jsDelivr --><script src="https://vox.cab/npm/@markbattistella/docsify-sidebarfooter@latest"></script><!-- locally --><script src="docsify-sidebarfooter.min.js"></script>
```

复制

然后是配置参数

```
<script>window.$docsify = {  autoFooter: {    name:       String,          // company display name (required)    copyYear:   Int,             // start copyright year (required)    url:        String,          // company url (optional)    policy:     Bool | String,   // show Privacy Policy (optional)    terms:      Bool | String,   // show Terms of Service (optional)    cookies:    Bool | String,   // show Cookies Policy (optional)    onBody:     Bool             // if true it is on the main doc  }};</script>
```

复制

*   `name`就是填写公司的名字，填写的时候要记得加引号
*   `copyYear`就是年份，填写的时候不需要加引号
*   `url`就是网站链接，填写的时候要记得加引号

底下就是一些关于其他信息的设置，可以选择开启并选择md的路径。

不过不知道cookies之类的格式应该怎么写。

但是到了现在，其实侧边栏还没有出现页脚的信息，我们还需要

在`index.html`的`body`标签里添加

```
<footer id="mb-footer"></footer>
```

复制

然后去`_sidebar.md`文件里面也添加上一行代码

### 侧边栏插件[docsify-sidebar-collapse](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FiPeng6%2Fdocsify-sidebar-collapse)

Support docsify sidebar catalog expand and collapse.

这是我最要的功能了，它提供了给侧边栏进行多级分类，并且自动折叠，然后有两种展示的风格。

![](https://ask.qcloudimg.com/http-save/7689800/d06e03b7f3b812a49e293ffd8595b31e.png)

![](https://ask.qcloudimg.com/http-save/7689800/ddc0517ce9270370af9f9a533f4ff8f8.png)

其实风格二会比较明显的，只是那个蓝色的文件夹跟整体的风格有点不搭，要是我会自定义就好了。

接下来就是安装插件的过程

**首先当然也是加载js**

```
<script src="//vox.cab/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
```

复制

**接下来是风格的选择，放到`head`标签里**

*   风格一

```
<link rel="stylesheet" href="//vox.cab/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
```

复制

*   风格二

```
<link rel="stylesheet" href="//vox.cab/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />
```

复制

**最后就是在`_sidebar.md`里面对目录进行一个书写了**

首先最基本的，就是通过不同的缩进确定分级，如下：

```
- 一级目录    - 二级目录        - 三级目录
```

复制

![](https://ask.qcloudimg.com/http-save/7689800/c0e83a1aabe82b328209b4a216e8f506.png)

我们可以观察到，最底层的目录的图标有点不一样，以上是展开的效果。

添加文档的话。一般会有两种习惯的写法。

*   文档永远放在最底层目录，文档这个层级不会出现子分类

```
- 一级目录    - 二级目录1        - 三级目录1            - [文档]        - 三级目录2            - [文档]            - [文档]        - 三级目录3            - [文档]    - 二级目录2        - 三级目录            - [文档]
```

复制

![](https://ask.qcloudimg.com/http-save/7689800/ef0101323c6875eaafa4ceb320b27ff7.png)

*   文档不是最底层目录，文档下还有子分类

```
- 一级目录    - 二级目录        - [文档](docs/1.md)        - [文档](docs/1.md)        - 三级目录            - [文档](docs/1.md)            - [文档](docs/1.md)
```

复制

> 这种写法有时候容易起冲突，第一次试的时候，可能是其他的js之间影响了，或者说没配置好，结果侧边栏乱七八糟。 第二次尝试的时候把多于的插件删掉了，当然也有可能是我子目录放在同级文档下的原因，总之写一下尝试一下就知道了。

* * *

**默认展开的层级设置**

我们在配置参数中添加

```
sidebarDisplayLevel: 0
```

复制

*   数字0就代表不展开 只显示最表层的【一级目录】
*   数字1的话就会展开二级目录。如下图：

![](https://ask.qcloudimg.com/http-save/7689800/22c1b72560fc08deb4492e86723c6e04.png)

### 绘图[websequencediagrams-docsify](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Faajiwani%2Fwebsequencediagrams-docsify)

A plugin to embed WebSequenceDiagrams right into your documentation.

docsify-material-icons - Add Material Icons to documentation by tokens.

好像也是一个绘图插件，不是很懂~

### Material ico[docsify-material-icons](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Ferickjx%2Fdocsify-material-icons)

Add Material Icons to documentation by tokens.

这跟fontawesome一样是一个图标库

### 广告位[docsify-ethicalads](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fdavidjcralph%2Fdocsify-ethicalads)

EthicalAds support for Docsify.

这好像是放广告位的地方~哈哈哈哈！

### [docsify-wikilink](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fzpengg%2Fdocsify-wikilink)

A plugin that allows wiki internal link syntax by using double square brackets like \[pagename|link text\].

这个插件我真的放弃了，看上去感觉还挺简单，实际上没懂。

### 链接预览[docsify-link-preview](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fpuria%2Fdocsify-link-preview)

A plugin to render link previews.

连接预览？我猜测就是把鼠标放到网站上，然后它就会有一个浮窗，预览网站内容~

不过这个安装需要去别的地方申请api~我就先不弄了。

### [docsify-pseudocode](/developer/tools/blog-entry?target=https%3A%2F%2Fh-hg.github.io%2Fdocsify-pseudocode%2F%23%2F)

A plugin to render pseudocode in docsify. @h-hg

说是什么伪代码?也是我看不懂的玩意

### 页脚信息[docsify-footer](/developer/tools/blog-entry?target=https%3A%2F%2Falertbox.github.io%2Fdocsify-footer%2F%23%2F)

A markdown _footer.md plugin for docsify-enabled sites. @alertbox.

这个页脚信息感觉比上面那个侧边栏页脚要更加的适合我用。

![](https://ask.qcloudimg.com/http-save/7689800/5b56a3cb328db8d2e35b7e63a4173d7f.png)

这是人家官方的效果，实际上是读取了一个md文件所以相对来说自定义程度要高很多。

首先是加载js

```
<script src="//vox.cab/npm/@alertbox/docsify-footer/dist/docsify-footer.min.js"></script>
```

复制

> **这里一定要非常非常的注意！** 一定要放在docsify自己的js依赖下方 我一开始还以为位置、顺序是无所谓的，实际上页脚信息会加载不出来

接着是配置参数

```
window.$docsify = {  loadFooter: true,  loadFooter: '_footer.md',};
```

复制

其实就是两个参数，第一个是打开页脚功能，第二个是指定一个页脚的md文件，名字可以自定义。

大概就是这样了~

### [docsify-code-inline](/developer/tools/blog-entry?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2F%40rakutentech%2Fdocsify-code-inline)

Enables syntax highlighting for inline code as well, not just code fences. Never again will inline code look dull. @rakutentech

额~也是跟什么代码啥的有关系

### 备案信息[docsify-beian](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FHerbertHe%2Fdocsify-beian)

A plugin to add Chinese Beian Information in docsify. @HerbertHe

docsify-progress - A plugin to render reading progress in docsify. @HerbertHe.

这是一个中文文档，其实不错的，添加[备案](https://cloud.tencent.com/product/ba?from_column=20065&from=20065)号非常的方便，但是...

![](https://ask.qcloudimg.com/http-save/7689800/1f3157071c6640a44a4f5474de2ba5fb.png)

这么来说的话，我可能还是会选择上面那个页脚插件，因为自由度会更高一点。

### 阅读进度条[docsify-progress](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FHerbertHe%2Fdocsify-progress)

A plugin to render reading progress in docsify. @HerbertHe.

> 这个插件与`字数插件`不兼容

这也是一个中文文档，会在页面顶部或者最底部出现一个根据阅读进度改变的横条。颜色、横条的粗细、位置都可以自定义。

![](https://ask.qcloudimg.com/http-save/7689800/054dd241f0f4c4c75408a5b83d59102b.jpg)

首先是加载js

```
<script src="https://vox.cab/npm/docsify-progress@latest/dist/progress.min.js"></script>
```

复制

然后是配置参数

```
window.$docsify = {
    progress: {
        position: "top",
        color: "var(--theme-color,#42b983)",
        height: "3px",
    }
}
```

复制

很明显，从上到下就是`位置`、`颜色`、`横条粗细`的自定义

### iframe嵌入[docsify-codeblock-iframe](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FHerbertHe%2Fdocsify-codeblock-iframe%2Fblob%2Fmain%2FREADME.CN.md)

A plugin to provide markdown extra codeblock-iframe syntax support for docsify, just for supporting iframe rendering securely. @HerbertHe.

哈哈 这个也有中文文档~可以自行去看一下，是关于什么iframe嵌入之类的~、

### 绘图[docsify-kroki](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fzuisong%2Fdocsify-kroki)

A plugin to integration kroki into docsify. @zuisong.

这个也是个作图软件，好像跟上面提到的plantuml以及mermaid都有点关系~

### 绘图[docsify-charty](/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2Fmarkbattistella%2Fdocsify-charty)

Add some charts and graphs to your docsify website. Pie charts, doughnut charts, sectional, bar and column graphs, line and plot graphs, and a review block. Everything you need if you need to visualise some numbers!

这也是专门做图表的工具~

原创声明：本文系作者授权腾讯云开发者社区发表，未经许可，不得转载。

如有侵权，请联系 [cloudcommunity@tencent.com](mailto:cloudcommunity@tencent.com) 删除。

[java](/developer/tag/10164)

[html](/developer/tag/10205)

[markdown](/developer/tag/10757)

[网站](/developer/tag/10548)

[编程算法](/developer/tag/10663)

原创声明：本文系作者授权腾讯云开发者社区发表，未经许可，不得转载。

如有侵权，请联系 [cloudcommunity@tencent.com](mailto:cloudcommunity@tencent.com)删除。

[java](/developer/tag/10164)

[html](/developer/tag/10205)

[markdown](/developer/tag/10757)

[网站](/developer/tag/10548)

[编程算法](/developer/tag/10663)