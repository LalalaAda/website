---
title: 面试 2020 07
date: 2020-07-28 17:19:06
tags:
---
## JS原型
{% asset_img 原型.jpg js原型图 %}
参考地址： {% link JavaScript之原型链的解读 https://www.jianshu.com/p/a9887fc15285 JavaScript之原型链的解读 %}
## JS原型继承
{% codeblock  lang:javascript %}
// 最佳寄生组合式继承
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
function prototype(child, parent) {
  var prototype = object(parent.prototype);
  prototype.constructor = child;
  child.prototype = prototype;
}
prototype(Child, Parent);
{% endcodeblock %}
<details>
  <summary>多种继承方式详情</summary>
  {% codeblock  lang:javascript %}
  // 1.原型链继承
  function Parent() {
    this.name = 'tom'
  }
  Parent.prototype.getName = function () {
    console.log(this.name);
  }
  function Child () {}
  Child.prototype = new Parent();
  var c1 = new Child();
  console.log(c1.getName()); //tom
  {% endcodeblock %}
</details>

参考地址：[JavaScript深入之继承的多种方式和优缺点](https://github.com/mqyqingfeng/Blog/issues/16)

