---
title: 模块化系列（二）：现有前端模块化规范介绍
date: 2016-12-29 11:38:59
tags: 
 - JavaScript
 - 模块化
 - 标准规范
categories:
 前端技术
---

在阮一峰的博文[《Javascript模块化编程（一）：模块的写法》](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)中描述了对前端模块化实现思路的基本演进过程。

现有的较为成熟的前端模块化规范有CMD（Common Module Definition，通用模块定义）、AMD（Asynchronous Module Definition，通用模块定义）以及CommonJS，这些规范都是由于ES5（尤其是前端的JavaScript）不支持模块化编程而设计的解决方案。在ES6中正式定义“类”和“模块”，在语言规范层面支持模块化编程。

CMD和AMD是较早的为实现前端模块化定义的规范，目前正处于淘汰阶段，连SeaJS的作者玉伯也说*该给SeaJs立一块墓碑了*。

![Sea.js](http://seajs.org/docs/assets/images/logo.png)
>[CMD](https://link.zhihu.com/?target=https%3A//github.com/seajs/seajs/issues/242) 是 [SeaJS](http://seajs.org/) 在推广过程中对模块定义的规范化产出。


![RequireJS](http://requirejs.org/i/logo.png)
>[AMD](https://link.zhihu.com/?target=https%3A//github.com/amdjs/amdjs-api/wiki/AMD) 是 [RequireJS](http://requirejs.org/) 在推广过程中对模块定义的规范化产出。

上两句是玉伯对两种规范的概括。

CMD、AMD规范的比较见知乎上玉伯对[《AMD和CMD的区别有哪些？》](https://www.zhihu.com/question/20351507/answer/14859415)的回答，以及[《与 RequireJS 的异同》](https://github.com/seajs/seajs/issues/277)。
