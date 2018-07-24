近1年多以来，开发vue项目是我的主要工作，再有便是开发各种活动页面、内嵌h5、webApp 之类的工作。许是代码写的多了，对原有的疑惑点也自然而然的想通了，应了那位伟人说的话：“实践出真理！”。

#### 回首篇
* 作用域
   + 关于如何解释作用域，我一直找不到很正经的解释。“根据名字找变量的规则。”姑且这样解释
   + 作用域链：在此规则下，如果在当前作用域内没有找到该变量，就向外外层作用域查找，直到全局作用域，如果还没有找到就报错。

* 词法作用域
   + 编写代码的时候变量和函数写在哪就由哪里来决定。
   + 在词法解析器解析代码的时候能极大的保证作用域不变。

* 变量提升
  + 在语法解析阶段，变量声明及函数被提升至当前作用域最顶端；
  + 其中变量，在代码未执行时值为`undefined`;
  ```js
    console.log(a) // undefined
    var a = 10
  ```
  + 同时，用let声明的变量在代码未运行到之前一直都是”不存在“。
  ```js
  console.log(a) // ReferenceError: a is not defined
  let a = 10
  ```
* 闭包
  + 常规版：能够读取其他函数内部变量的函数。
  + 个人版：词法作用域之外调用，保持对原有作用域内变量的访问。
  ```js
    function foo () {
        var a = true
        // 词法作用域
        return function bar () {
            console.log(a)
        }
    }
    var base = foo()
    base() // true  全局作用域调用
  ```
* 匿名函数
  + 保证内部私有变量，不被外部变量污染且可自执行的函数。- 函数作用域
  + 观察的jQuery 之类的框架都是使用匿名函数;
  + 在了解足够后，开发Query.js;
  + IIFE，立即执行函数表达式
  ```js
  ;(function () {
     var Q = {
         version: 1.0.0
     } 
     Q.islogin = function () {}
     return window.Query = Q
  })()
  ```
* this
  + 但凡是个前端，这都是绕不开的一个环节。
  + this，执行上下文，使用this的情况更像是动态作用域
  + 与词法作用域不同，this更关乎的是在函数在**哪**调用了，当然，call , apply, bind 都是可以改变this的指向，那就驳论了。
  + 实际中，this应该是在执行中绑定的。
  + 在我的实际编码过程中，有时对动态作用域困惑时，我还是选择自己最熟悉的词法作用域；如下
  + 既然用到`=>`箭头函数了，箭头函数中实际并没有this，其内部的this实际上就是外层块所在的作用域；
  ```js
    function foo () {
        var self = this
        setTimeout(() => {
            self.code = 200
        }, 1000)
    } 
  ```
* 深浅拷贝
  + 在我当前的项目中为实没有遇到过类似对象的拷贝问题，但是既然是回首那就写一写；
  ```js
    function simpleClone (obj) {
        var newObj;
        if (typeof obj === 'object') {
            newObj = obj instanceof Array ? [] : {}
            for (var key in obj) {
                if (obj.hasOwnProperty(key)) {
                    newObj[key] = obj[key];
                }
            }
        } else {
            newObj = obj
        }
        return newObj
    }

    function deepClone (obj) {
        var newObj;
        if (typeof obj === 'object') {
            newObj = obj instanceof Array ? [] : {}
            for (var key in obj) {
                if (obj.hasOwnProperty(key)) {
                    newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key]
                }
            }
        } else {
            newObj = obj
        }
        return newObj
    }
  ```
  + 当然以上的clone均为乞丐版，完全版是[stack overflow 一条精彩的回答](https://stackoverflow.com/questions/728360/how-do-i-correctly-clone-a-javascript-object)
* 原型
  + 对象`__proto__`，函数`prototyoe`
  + 当然两者都是object，也印证了那句话："看得到的都是对象。"
  + 原型链，我个人的感觉就像和作用域链一样，寻找属性(方法)的规则
* 关于Vue的初阶
    我写了一篇关于vue-cli的入门在[这里](https://github.com/Yinlongcoding/about_vue-cli)，看看就好，有错误的话私聊哈~
