# HTML/CSS Sytle Guide - HTML/CSS 编码规范

## 简介

## HTML 规范

### 代码规范

**所有 HTML 标签都小写**

    <ul>
        <li><a target="_blank" href="https://github.com/" title="GitHub">GitHub</a></li>
        <li><a target="_blank" href="//www.google.com">Google</a></li>
    </ul>

**使用 HTML5 的 doctype**

    <!doctype html>

**页面编码用 utf-8**

没有特殊说明或要求，页面编码默认都用 `utf-8` 编码，有些需要使用 `gb2312` 编码的，用 `gbk`，它是 `gb2312` 的扩展，而且向后兼容，具有更好的兼容性。

    <meta charset="utf-8">

页面语言 lang 使用 zh-Hans-CN

    <html lang="zh-Hans-CN">

`zh` 和 `zh-CN` 均属于废弃用法。 与中文有关的 lang 值如下：

* `zh-Hans` 简体中文

* `zh-Hans-CN` 大陆地区使用的简体中文

* `zh-Hans-HK` 香港地区使用的简体中文

* `zh-Hans-MO` 澳门使用的简体中文

* `zh-Hans-SG` 新加坡使用的简体中文

* `zh-Hans-TW` 台湾使用的简体中文

* `zh-Hant` 繁体中文

* `zh-Hant-CN` 大陆地区使用的繁体中文

* `zh-Hant-HK` 香港地区使用的繁体中文

* `zh-Hant-MO` 澳门使用的繁体中文

* `zh-Hant-SG` 新加坡使用的繁体中文

* `zh-Hant-TW` 台湾使用的繁体中文

### 文件命名

文件扩展名必须为 .htm 或 .html

index.html 引导页&首页
list.html 列表页
article.html 文章页
download.html 下载页面
act.html 活动列表页面
video.html 视频
文件名中只可由英文字母a~z、排序数字0~9或间隔符-组成。
件名中禁止包含特殊符号，比如空格、$等
文件名区分大小写，统一使用小写字母
为更好的表达语义，文件名使用英文名词命名，或英文简写。

### 图片

图片格式/大小

图片格式：图片允许采用gif/jpg/png/wep ，平衡图片质量与文件大小，适当运用 css sprite 理念合并修饰类图片，不过分损失质量情况下尽量减小页面下载数据量。 图片单张体积不能超过150K，jpg图片必须压缩，一般60%品质即可，如果图片质量不好，可提高到80%

图片引用

图片路径需要使用绝对路径方式;
旧版页面中CSS维护仍可在webplat采用相对路径方式修改发布（备注）;
所有img元素必须加上alt属性，修饰性图片alt属性内容留空，内容性质图片alt属性写相应内容;
必须加上width和height属性，值为它的原大小，但不要用来对它进行缩放。

图片命名

图片后缀命名一律小写。
使用间隔符-进行连接。*一般背景图片以bg-开头，测试图片以img-开头，按钮图片以btn-开头，图标图片以icon-开头，聚合图以spr-开头，后跟英文单词，不推荐使用汉语拼音，如果名称过长，适当使用缩写

bg-body.jpg spr-home.png img-promo.jpg btn-submit.png  icon-game.png

### 注释

正确的注释规范：

感叹号后面2个横线，结束时2个横线； 不要在注释内容中使-- ，--只能发生在XHTML注释的开头和结束，也就是说，在内容中它们不再有效。 例如下面的代码是错误的:

    <!--这里是注释     -这里是注释-->
    <!--    -这里是注释     -这里是注释    --->

用等号或者空格替换内部的虚线,这样是正确的

    <!--这里是注释============这里是注释-->

IE条件注释（IE10已不支持条件注释）

    <!-- [if IE]>
    这里只有ie浏览器才可以显示
    <![endif]-->
 
    <!-- [if !IE]>
    这里只有非ie浏览器才可以显示
    <! <![endif]-->
 
    <!--[if IE 6]>
    这里只有ie6浏览器才可以显示
    <![endif]-->
 
    <!--[if lt IE 9]>
    这里只有ie9以下浏览器才可以显示
    <![endif]-->
 
    <!--[if lte IE 8]>
    这里只有ie8以及ie8以下浏览器才可以显示
    <![endif]-->

### 脚本中文转 Unicode

为防止外链脚本未申明正确编码导致乱码的问题，脚本中如用到中文，必须转为unicode码

    /* 不推荐 */
    document.write("关于")
    /* 推荐 */
    document.write("\u5173\u4e8e")

### 去掉类型属性

不要为CSS、JS使用类型属性，特别说明类型（type）属性是多余的，在HTML5中默认已包含

    <!--不推荐-->
    <link href="../css/comm.css" rel="stylesheet" type="text/css" />
    <script type="text/javascript"><!--mce:0--></script>
    <script src="common.js" type="text/javascript">

    <!--推荐-->
    <link href="../css/comm.css" rel="stylesheet" />
    <script type="text/javascript"><!--mce:1--></script>
    <script src="common.js">

### 对“<”“>”之类的符号进行实体转义

在 HTML 中不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）

    <!--不推荐-->
    <a href="/wiki/">more>></a>
    <!--推荐-->
    <a href="/wiki/">more&gt;&gt;</a>

https://dev.w3.org/html5/html-author/charref

### 元素嵌套规范

段落元素与标题元素只能嵌套内联元素

    <!--不推荐-->
    <a><p> </p><div></div><p> </p></a>  <h2><div></div></h2>
    <!--推荐-->
    <p><span><span> </span></span></p>
    <h2><span> </span></h2>

## CSS 规范

### 命名规范

使用类选择器，尽量避免使用ID选择器定义样式

ID在一个页面中的唯一性导致了如果以ID为选择器来写CSS，就无法重用。

以字母开头

必须以字母开头命名选择器，这样可保证在所有浏览器下都能兼容；
不允许单个字母的类选择器出现；
不允许命名带有广告等英文的单词，例如ad,adv,adver,advertising，已防止该模块被浏览器当成垃圾广告过滤掉。任何文件的命名均如此。
全小写，并使用 ' - ' 连字符

下划线 ' _ ' 禁止出现在class命名中，统一使用'-'连字符
禁止驼峰式命名
命名应简约而不失语义

避免过度简写，.ico足够表示这是一个图标，而.i不代表任何意思
使用有意义的名称，使用结构化或者作用目标相关的，而不是抽象的名称

文件命名举列

基本样式：base.css框架布局：layout.css模块样式：module.css全局样式：global.css字体样式：font.css首页样式：index.css 链接样式：link.css打印样式：print.css

### 常用类/ID命名举列

常用类的命名应尽量以常见英文单词为准，做到通俗易懂，并在适当的地方加以注释。 部分命名解释约定： 整页.wp 页眉.header 页脚.footer 导航.nav 主体内容.main侧边栏.side 标志.logo搜索.search登录.login注册.reg标题.tit-...副标题.subtit-... 按钮.btn-...链接.link-... 背景图片.bg-...列表.list-... 表格.tb-...标签.tag-... 视频.video-...联系.contact

### CSS Reset

Eric Meyer’s “Reset CSS” 2.0
http://cssreset.com/scripts/eric-meyer-reset-css/

Normalize.css
http://necolas.github.io/normalize.css/

CSS 属性值需要用到引号时，统一使用单引号

    /* 不推荐 */
    selectors{ font-family:"\5FAE\8F6F\96C5\9ED1";}
    
    /* 推荐 */
    selectors{ font-family:'\5FAE\8F6F\96C5\9ED1';}

为单个 CSS 选择器或新申明开启新行

    /* 不推荐 */
    .home-count .hd,.content-title,.select-game-title .title{}.nav{}
    
    /* 推荐 */
    .home-count .hd,
    .content-title,
    .select-game-title .title{}
    .nav{}

### CSS 属性书写顺序

建议遵循：布局定位属性 自身属性 文本属性 其他属性 CSS3属性 mozilla官方属性顺序推荐

    /* 这些属性只是最常用到的, 并不代表全部 */
    /* 布局定位属性 */
    display / list-style / position（相应的 top,right,bottom,left） / float / clear  / visibility / overflow
    /* 自身属性 */
    width / height / margin / padding / border / background
    /* 文本属性 */
    color / font / text-decoration / text-align / vertical-align / white- space / break-word
    /* 其他（CSS3）  */
    content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient ...

**CSS 浏览器私有前缀书写格式**

selectors{
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#ffffff), color-stop(100%,#eff2f4));
    background: -webkit-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: -moz-linear-gradient(top, #ffffff 0%, #eff2f4 100%);
    background: -ms-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: -o-linear-gradient(top, #ffffff 0%,#eff2f4 100%);
    background: linear-gradient(to bottom, #ffffff 0%,#eff2f4 100%);
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#eff2f4',GradientType=0 );
}

**不要以没有语义的标签作为选择器**

    /* 不推荐 */
    .m-xxx div{ ... }

**CSS 单行书写法（根据个人习惯选择）**

每个CSS选择符的主申明区中的属性在同一行内书写，每个属性之间空一格

**CSS 多行书写法（根据个人习惯选择）**

每个CSS选择符的主申明区中的每一条属性新起一行

    selectors{
        height: 30px;
        padding-bottom: 10px;
        border-bottom: 1px solid #858585;
        margin-bottom: 10px;
    }

### 注释

**行间注释**

直接写于属性值后面，如：

    .search{background: #333 url(../img/search.gif) no-repeat;/*定义搜索框的背景*/}

**整段注释**

分别在开始及结束地方加入注释，如：

    /*=====搜索条=====*/
    .search {background: #333 url(../img/search.gif) no-repeat;}
    /*=====搜索条结束=====*/

注意：以下写法不可取

    .news/* 这里是高度自动撑 */ {line-height:1.5}
    .news {/*line-height:1.5 这里是高度自动撑 */}

### Hack

原则上不允许使用Hack - 很多不兼容问题可以通过改变方法和思路来解决，并非一定需要Hack，根据经验你完全可以绕过某些兼容问题。 - 一种合理的结构和合理的样式，是极少会碰到兼容问题的。 -由于浏览器自身缺陷，我们无法避开的时候，可以允许使用适当的Hack。

**统一Hack方法**

    .element{
    color:#000;             /*w3c标准*/
    [;color:#f00;];         /*Webkit(chrome和safari)*/
    color:#666\9;           /*IE8*/
    *color:#999;            /*IE7*/
    _color:#333;            /*IE6*/
    }
    :root .element{color:#0f0\9;}  /*IE9*/
    @media all and (-webkit-min-device-pixel-ratio:10000), not all and (
    -webkit-min-device-pixel-ratio:0) { .element{color:#336699;}}  /*opera*/
    @-moz-document url-prefix(){ .element{color:#f1f1f1;}} /*Firefox*/

**简写 CSS 颜色属性值**

    /* 不推荐 */
    selectors{ color:#000000; background-color:#ddeeff;}
    /* 推荐 */
    selectors{ color:#000; background-color:#def;}

**删除 CSS 属性值为 0 的单位**

0就是0，任何单位都不需要w3c关于属性单位的说明

    /* 不推荐 */
    selectors{ margin:0px; padding:0px;}
    /* 推荐 */
    selectors{ margin:0; padding:0;}

### 删除无用CSS样式

第一，删除无用的样式后可以缩减样式文件的体积，加快资源下载速度；第二，对于浏览器而言，所有的样式规则的都会被解析后索引起来，即使是当前页面无匹配的规则。移除无匹配的规则，减少索引项，加快浏览器查找速度；

    /* 不推荐 */
    selectors{ font-size:12px;}
    .nav{}
    .nav-item{ height:20px;}
    /* 推荐 */
    selectors{ font-size:12px;}
    .nav-item{ height:20px;}

