#### 前言
为什么写这么一个东西？即将离职，一年多了总找不到什么好的机会去总结，如今空闲下来，便一下写个痛快；都写了些啥？前端方面的个人总结(包含吐槽)。有啥想说的？最好别被人发现，发现了就看看就行。工作期间使用的是Vue.js，更多的时候我在写移动端，所以兼容的事情，很少去考虑。

> 许是，越是简单的事情就越怕做的不好。记我键盘下的HTML

“HTML这门语言很简单。”这句话是我的同行或者刚对此有兴趣并了解的人经常说的话，确实它非常简单，很包容。哪怕你的结构或者嵌套是错误的，它依旧能展示出来。我在刚接手公司项目的时候看到过如下HTML代码：
```HTML
    <div class="box">
        <span class="container">
            <div class="item">one</div>
            <div class="item">two</div>
        </span>
    </div>
```
哭笑不得就是当时的表情。所幸正常展示了信息。

##### 语义化
> 粗浅的话便是：“在合适的地方用上合适的嵌套，在合适的嵌套里用上合适的标签。”至少我是这么认为。
在后来的重构中，上面那段代码被修改为如下代码：
```HTML
    <div class="box">
        <div class="container">
            <div class="lists">
                <span class="item">one</span>
                <span class="item">two</span>
            </div>
        </div>
    </div> 
```
##### 结构
> 著名的[Yahoo军规](https://github.com/creeperyang/blog/issues/1)中提出，*减少DOM元素数，减少代码体积* 我的重构版完全违背了这个原则，具体原因如下：

结构本就是拿来梳理关系的，HTML的结构亦是如此；加上一层lists是为了以后的可扩展性，如果日后需求改变，怕是我已经不记得当时的代码是怎么写的了。具体涉及CSS的问题，且留在下一篇。

##### 多样化的mate
mate标签一个神奇的标签，从常用的viewport到各种浏览器的适配等作用，看了Google FaceBook等添加了不少mate标签但具体是用作什么还是未知。
只列出一些，我知道的。当然这是在[segmentfault](https://segmentfault.com)里某位热心老哥的回复。如下：
```HTML
    <meta charset="UTF-8">
    <!-- 视图窗口，移动端特属的标签。 -->
    <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no" />
    <!-- 是否启动webapp功能，会删除默认的苹果工具栏和菜单栏。 -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <!-- 这个主要是根据实际的页面设计的主体色为搭配来进行设置。 -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <!-- 忽略页面中的数字识别为电话号码,email识别 -->
    <meta name="format-detection" content="telephone=no, email=no" />
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 避免IE使用兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app"> 
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
```
因为经常需要写内嵌的h5，这些mate能够很好的帮助我处理个别的一些浏览器的倔脾气，巴适得很~
