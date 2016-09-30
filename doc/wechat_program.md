title: 微信小程序
speaker: Jason Hou
transition: slide
theme: dark
transition: zoomin
[slide]
# 微信小程序设计
[slide]
## MVVM
----
![](http://image.beekka.com/blog/2015/bg2015020110.png)

[slide]

## MVVM的微信框架MINA
----
![](/img/wechat_mvvm.png)

[slide]
## 目录结构
----
<pre>
<code class="Markdown">
├── app.js
├── app.json
├── app.wxss
├── models
├── pages
├── utils
└── vendor
</code>
</pre>

[slide]
## 生命周期
----
![](https://mp.weixin.qq.com/debug/wxadoc/dev/image/mina-lifecycle.png?t=1475052056717)
[slide]
## 模块化
----
CommonJS
<pre>
<code class="javascript">
  // sum.js
  module.exports = function (a, b){
    return a + b;
  }
  // main.js
  var sum = require('./sum.js');
  sum(1, 2);
</code>
</pre>



[slide]
## 第三方库
----
- 不能使用任何与DOM有个的库
- 不支持CommonJs 模块规范的库
- 就是满足上面两天你也不一定
[slide]

## 解决办法
[slide]

手动修改第三方库
<pre>
<code class="javascript">
  module.exports = (function (){
    var root = this;
      .....
    return root;
  }.call(this));
</code>
</pre>

[slide]
## 模块引用
----
准备踩坑
[slide]
----
## 只能在Pages中引用

[slide]

# 谢谢大家
