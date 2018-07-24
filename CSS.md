在我的感觉里，觉得CSS这门语言很难掌握。不过，根据不同的需求，所需要的文档资料都是在一定范围内的，再加上社区方面不断贡献出优秀的 CSS 库和精致的UI库，让我在项目中 CSS 写的并不多。但在重构一些老项目时，还是留下一些自己的理解。

##### 布局
> 遵循以下规则：尽量多的使用常规流(normal flow)，尽量少的触发回流(reflow)和重绘(repaint)。

###### float
+ 在重构过程中遇到最多布局是浮动，相比较而言，浮动布局的代码确实多了点，一旦浮动就要闭合浮动；
+ 更多的时候`display: inline-block;`相同的效果；
+ 使用伪元素来闭合浮动；

###### position
+ 一个有趣的现象：dialog(遮罩层)。这样就无需设定遮罩层的高度和宽度，如下：
```html
 <div class="dailog">dailog</div>
 <style>
    .dailog {
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background: rgba( 0, 0, 0, 0.33)
      }
</style>
```
+ 但是，你以为`fixed`就真的那么好用？
在移动端上，尤其是菊花厂(华为)手机的touch tools按钮会完全覆盖在你视口定位在最下方的按钮。
解决方案：1、安卓工程师写兼容，2、加上约40px的padding-bottom; 我倾向于第一种

###### Transform和负margin的选择
  + 无论是开启GPU加速，无回流都是很好的体验。
  + 当然，无论是使那个都要注意元素是在实际的进行偏移。会影响到其他元素。
```html
 <style>
     /* 开启GPU加速 */
    .dom {
        webkit-transform: translate3d(0,0,0);
        -moz-transform: translate3d(0,0,0);
        -ms-transform: translate3d(0,0,0);
        -o-transform: translate3d(0,0,0);
        transform: translate3d(0,0,0);
      }
</style>
```

###### flex
+ 目前flex是我的首选布局方案，代码量和适应性都是很好的；
+ 随着当前兼容性日渐减少，flex将会是布局首选；

###### CSS Tools
+ 公司项目中使用Sass，但是node-sass的download一直都是个毒瘤。在不同环境下，如Linux环境下的node-sass又会是另外一个问题；
+ 在前端多元化的今天，[postCSS](https://postcss.org/)是我一直想想在项目中使用的。

##### CSS静态资源
一个活动页面，可能需要加载不少image和js，在没有CDN的情况下，压缩CSS 代码和 js代码是个不错的选择。`VS Code` 编译器提供 `Minify插件`一键式压缩代码。
