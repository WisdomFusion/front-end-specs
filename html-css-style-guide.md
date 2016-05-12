# HTML/CSS Sytle Guide - HTML/CSS 编码规范

## 1. 简介

本文整理的 HTML/CSS 编码规范，为的是让团队成员都能编写灵活、稳定、高质量的 HTML 和 CSS 代码，而不是为了限制或约束。

## 2. HTML 规范

### 2.1 代码规范

**所有 HTML 标签都小写**

```html
<ul>
    <li><a target="_blank" href="https://github.com/" title="GitHub">GitHub</a></li>
    <li><a target="_blank" href="//www.google.com">Google</a></li>
</ul>
```

**使用 HTML5 的 doctype**

```html
<!doctype html>
```

**页面编码用 utf-8**

没有特殊说明或要求，页面编码默认都用 `utf-8` 编码，有些需要使用 `gb2312` 编码的，用 `gbk`，它是 `gb2312` 的扩展，而且向后兼容，具有更好的兼容性。

```html
<meta charset="utf-8">
```

**页面语言 lang 使用 `zh-CN`**

根据 HTML5 规范：

    强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

```html
<html lang="zh-CN">
    <!-- ... -->
</html>
```

### 2.2 文件命名

文件扩展名必须为 `.htm` 或 `.html`，PHP 框架模板除外：

* index.html 引导页&首页
* list.html 列表页
* article.html 文章页
* download.html 下载页面
* act.html 活动列表页面
* video.html 视频
* 文件名中只可由英文字母`a~z`、排序数字`0~9`或间隔符`-`组成。
* 件名中禁止包含特殊符号，比如`空格`、`$`等
* 文件名区分大小写，统一使用**小写字母**
* 为更好的表达语义，文件名使用英文名词命名，或英文简写。

### 2.3 图片

**图片格式/大小**

图片格式：图片允许采用 gif/jpg/png，平衡图片质量与文件大小，适当运用 css sprite 理念合并修饰类图片，不过分损失质量情况下尽量减小页面下载数据量。 图片单张体积不能超过 150K，jpg 图片必须压缩，一般 60% 品质即可，如果图片质量不好，可提高到 80%，一般 Photoshop 中输出 JPG 高质量即可达标。

**图片引用**

* 所有img元素必须加上 alt 属性，修饰性图片 alt 属性内容留空，内容性质图片 alt 属性写相应内容;
* 必须加上 width 和 height 属性，值为它的原大小，但不要用来对它进行缩放。

**图片命名**

* 图片后缀命名一律小写。
* 使用间隔符 `-` 进行连接。
* 一般背景图片以 `bg-` 开头，按钮图片以 `btn-` 开头，图标图片以 `icon-` 开头，聚合图以 `spr-` 开头，后跟英文单词，不推荐使用汉语拼音，如果名称过长，适当使用缩写。

如：bg-body.jpg, spr-home.png, btn-submit.png, icon-game.png

### 2.4 注释

**正确的注释规范**

* 感叹号后面2个横线，结束时2个横线；
* 不要在注释内容中使 `--`，`--` 只能发生在 XHTML 注释的开头和结束，也就是说，在内容中它们不再有效。

例如下面的代码是错误的:

```
<!--这里是注释     -这里是注释-->
<!--    -这里是注释     -这里是注释    --->
```

用等号或者空格替换内部的虚线,这样是正确的

```
<!--这里是注释============这里是注释-->
```

IE条件注释（IE10 已不支持条件注释）

```html
<!-- [if IE]>
这里只有 IE 浏览器才可以显示
<![endif]-->

<!-- [if !IE]>
这里只有非 IE 浏览器才可以显示
<! <![endif]-->

<!--[if IE 6]>
这里只有 IE6 浏览器才可以显示
<![endif]-->

<!--[if lt IE 9]>
这里只有 IE9 以下浏览器才可以显示
<![endif]-->

<!--[if lte IE 8]>
这里只有 IE8 以及 IE8 以下浏览器才可以显示
<![endif]-->
```

### 2.5 脚本中文转 Unicode

为防止外链脚本未申明正确编码导致乱码的问题，脚本中如用到中文，必须转为 Unicode 编码

```html
/* 不推荐 */
document.write("我们是前端攻城狮！")

/* 推荐 */
document.write("\u6211\u4eec\u662f\u524d\u7aef\u653b\u57ce\u72ee\uff01")
```

### 2.6 属性

**属性顺序**

HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

* `class`
* `id`, `name`
* `data-*`
* `src`, `for`, `type`, `href`
* `title`, `alt`
* `aria-*`, `role`

`class` 用于标识高度可复用组件，因此应该排在首位。`id` 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。

**去掉类型属性**

根据 HTML5 规范，在引入 CSS 和 JavaScript 文件时一般不需要指定 type 属性，因为 text/css 和 text/javascript 分别是它们的默认值。

```html
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

**布尔（boolean）型属性**

布尔型属性可以在声明时不赋值。XHTML 规范要求为其赋值，但是 HTML5 规范不需要。

更多信息请参考 [WhatWG section on boolean attributes](http://www.whatwg.org/specs/web-apps/current-work/multipage/common-microsyntaxes.html#boolean-attributes)：

元素的布尔型属性如果有值，就是 `true`，如果没有值，就是 `false`。

如果一定要为其赋值的话，请参考 WhatWG 规范：

如果属性存在，其值必须是空字符串或 `[...]` 属性的规范名称，并且不要再收尾添加空白符。

简单来说，就是不用赋值。

### 2.7 对“<”“>”之类的符号进行实体转义

在 HTML 中不能使用小于号（`<`）和大于号（`>`），这是因为浏览器会误认为它们是标签。如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（Character Entities）

```html
<!--不推荐-->
<a target="_blank" href="/site/">more >></a>

<!--推荐-->
<a target="_blank" href="/site/">more &gt;&gt;</a>
```

HTML 实例列表见看这里：[Character Entity Reference Chart](https://dev.w3.org/html5/html-author/charref)

### 2.8 减少标签的数量

编写 HTML 代码时，尽量避免多余的父元素。很多时候，这需要迭代和重构来实现。请看下面的案例：

```html
<!-- 不推荐 -->
<span class="avatar">
  <img src="...">
</span>

<!-- 推荐 -->
<img class="avatar" src="...">
```

### 2.9 元素嵌套规范

段落元素与标题元素只能嵌套内联元素

```html
<!--不推荐-->
<a><p></p><div></div><p></p></a>
<h2><div></div></h2>

<!--推荐-->
<p>
    <span><span></span></span>
</p>
<h2><span></span></h2>
```

## 3. CSS 规范

### 3.1 命名规范

**使用类选择器，尽量避免使用ID选择器定义样式**

ID在一个页面中的唯一性导致了如果以 ID 为选择器来写 CSS，就无法重用。

**以字母开头**

* 必须以字母开头命名选择器，这样可保证在所有浏览器下都能兼容。
* 不允许单个字母的类选择器出现。
* 不允许命名带有广告等英文的单词，例如 `ad`, `adv`, `adver`, `advertising`，已防止该模块被浏览器当成垃圾广告过滤掉。**任何文件的命名均如此。**

**全小写，并使用 `-` 连字符**

* 下划线 `_` 禁止出现在 class 命名中，统一使用 `-` 连字符。
* 禁止驼峰式命名。

**命名应简约而不失语义**

* 避免过度简写，`.ico` 足够表示这是一个图标，而 `.i` 不代表任何意思。
* 使用有意义的名称，使用结构化或者作用目标相关的，而不是抽象的名称。

**文件命名举列**

基本样式：`base.css`
框架布局：`layout.css`
模块样式：`module.css`
全局样式：`global.css` 或 `common.css`
字体样式：`font.css`
首页样式：`index.css`
链接样式：`link.css`
打印样式：`print.css`

### 3.2 常用类/ID命名举列

常用类的命名应尽量以常见英文单词为准，做到通俗易懂，并在适当的地方加以注释。class 名称中只能出现小写字符和 `-`（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名，部分命名及前缀参考下表：

| 名称       | 类名       | 名称     | 类名        |
|------------|------------|----------|-------------|
| 内容包裹器 | .wrapper   | 页眉     | .header     |
| 页脚       | .footer    | 导航     | .nav        |
| 迷你导航   | .mini-nav  | 顶部导航 | .top-nav    |
| 主体内容   | .main      | 侧边栏   | .sidebar    |
| 标志       | .logo      | 搜索     | .search     |
| 登录       | .login     | 注册     | .reg        |
| 标题       | .tit-...   | 副标题   | .subtit-... |
| 按钮       | .btn-...   | 链接     | .link-...   |
| 背景图片   | .bg-...    | 列表     | .list-...   |
| 表格       | .tb-...    | 标签     | .tag-...    |
| 视频       | .video-... | 联系     | .contact    |
| 地址       | .address   | 表单     | .frm-...    |

在为 Sass 和 Less 变量命名是也可以参考上面列出的各项规范，因为它们最终也是要编译为 CSS 的，可以多看看如 Bootstrap 之类的前端框架里的 CSS 类命名。

### 3.3 CSS Reset

* [Eric Meyer's "Reset CSS" 2.0](http://cssreset.com/scripts/eric-meyer-reset-css/)
  
  全部归零，这种 Reset 过于暴力，有些不该改变的样式也被改变，导致大量基础样式需要添加。

* [Normalize.css](http://necolas.github.io/normalize.css/)

  今后统一使用 Normalize.css，这也是 Bootstrap 使用的 Reset。

### 3.4 代码风格

**CSS 属性值需要用到引号时，统一使用单引号**

```css
/* 不推荐 */
selectors { font-family:"\5FAE\8F6F\96C5\9ED1"; }

/* 推荐 */
selectors { font-family:'\5FAE\8F6F\96C5\9ED1'; }
```

**为单个 CSS 选择器或新申明开启新行**

```css
/* 不推荐 */
.home-count .hd,.content-title,.select-game-title .title { } .nav { }

/* 推荐 */
.home-count .hd,
.content-title,
.select-game-title .title { }
.nav { }
```

**CSS 属性书写顺序**

相关的属性声明应当归为一组，并按照下面的顺序排列：

- Positioning
- Box model
- Typographic
- Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

完整的属性列表及其排列顺序请参考 [Recess](http://twitter.github.com/recess)。

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

**CSS 浏览器私有前缀书写格式**

```css
selectors {
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#ffffff), color-stop(100%,#eff2f4));
    background: -webkit-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: -moz-linear-gradient(top, #ffffff 0%, #eff2f4 100%);
    background: -ms-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: -o-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: linear-gradient(to bottom, #ffffff 0%,#eff2f4 100%);
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#eff2f4',GradientType=0 );
}
```

**选择器**

- 对于通用元素使用 class ，这样利于渲染性能的优化。
- 对于经常出现的组件，避免使用属性选择器（例如，`[class^="..."]`），浏览器的性能会受到这些因素的影响。
- 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 。
- 只有在必要的时候才将 `class` 限制在最近的父元素内（也就是后代选择器 `>`）。

```css
/* 不推荐 */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* 推荐 */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

**不要以没有语义的标签作为选择器**

```css
/* 不推荐 */
.m-xxx div { ... }
```

**CSS 单行书写法（根据个人习惯选择）**

每个CSS选择符的主申明区中的属性在同一行内书写，每个属性之间空一格

**CSS 多行书写法（根据个人习惯选择）**

每个CSS选择符的主申明区中的每一条属性新起一行

```css
selectors{
    height: 30px;
    padding-bottom: 10px;
    border-bottom: 1px solid #858585;
    margin-bottom: 10px;
}
```

### 3.5 注释

**行间注释**

直接写于属性值后面，如：

```css
.search { background: #333 url(../img/search.gif) no-repeat; /*定义搜索框的背景*/ }
```

**整段注释**

分别在开始及结束地方加入注释，如：

```css
/*==========login==========*/
.frm-login { }
/*==========//END login==========*/
```

注意：以下写法不可取

```css
.news /* 这里是高度自动撑 */ { line-height: 1.5 }
.news { /*line-height:1.5 这里是高度自动撑*/ }
```

### 3.6 不要使用 `@import`

与 `<link>` 标签相比，`@import` 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：

- 使用多个 `<link>` 元素
- 通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件

### 3.7 Hack

* **原则上不允许使用Hack！**
* 很多不兼容问题可以通过改变方法和思路来解决，并非一定需要 Hack，根据经验你完全可以绕过某些兼容问题。
* 一种合理的结构和合理的样式，是极少会碰到兼容问题的。
* 由于浏览器自身缺陷，我们无法避开的时候，可以允许使用适当的 Hack。

**统一Hack方法**

```css
.element {
    color:#000;             /*w3c标准*/
    [;color:#f00;];         /*Webkit(chrome和safari)*/
    color:#666\9;           /*IE8*/
    *color:#999;            /*IE7*/
    _color:#333;            /*IE6*/
}
:root .element { color:#0f0\9; }  /*IE9*/
@media all and (-webkit-min-device-pixel-ratio:10000), not all and ( -webkit-min-device-pixel-ratio:0) { .element { color:#336699; } }  /*opera*/
@-moz-document url-prefix(){ .element { color:#f1f1f1; } } /*Firefox*/
```

### 3.8 优化

**简写形式的属性声明**

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

- padding
- nmargin
- font
- background
- border
- border-radius

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

MDN（Mozilla Developer Network）上一片非常好的关于 [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。

```css
/* 不推荐 */
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

/* 推荐 */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

**删除 CSS 属性值为 0 的单位**

0就是0，任何单位都不需要 W3C 关于属性单位的说明

```css
/* 不推荐 */
selectors { margin:0px; padding:0px; }

/* 推荐 */
selectors { margin:0; padding:0; }
```

**删除无用CSS样式**

```css
/* 不推荐 */
selectors { font-size:12px; }
.nav { }
.nav-item { height:20px; }

/* 推荐 */
selectors { font-size:12px; }
.nav-item { height:20px; }
```
### 3.9 Less 和 Sass 中的嵌套

避免非必要的嵌套。这是因为虽然你可以使用嵌套，但是并不意味着应该使用嵌套。只有在必须将样式限制在父元素内（也就是后代选择器），并且存在多个需要嵌套的元素时才使用嵌套。

```css
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

## 4. Bootstrap 相关



