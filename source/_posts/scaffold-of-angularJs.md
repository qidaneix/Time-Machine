---
title: angular+webpack项目脚手架
date: 2017-03-19 21:37:53
tags:
 - JavaScript
 - AngularJs
 - 脚手架
categories:
 前端技术
---

# angular+webpack项目脚手架

*经过三个星期的webpack的学习（从2月7号到28号，好吧这是一篇迟到的博客），从对前端模块化的概念的一无所知到现在基本熟悉webpack2的使用方法，算是对前端模块化有了一定的掌握。可以说webpack给我一个全新的前端开发思路，webpack不单单是改变js代码的`<script>`标签顺序引入方式这么简单，它的“一切皆模块的”的思想对前端的开发、维护以及编译都有一个质的改变。我总结而来，它的最大优点和为人所青睐的原因是它的模块化思想增强了前端代码的可维护性；它的缺点是配置起来有一定难度，需要一定的学习成本（逃。。。我会在后面尝试讲解webpack的使用方法，不过要等到我可以熟练配置它的时候了。*

学会webpack后的第一件事，就是利用webpack配置了一个AngularJs(Angular1)的开发脚手架，并且将它挂在了github上，以便日后使用，项目地址：

**[web-project-template-angular](https://github.com/qidaneix/web-project-template-angular)**

下面是项目说明

本工程为基于angular框架的前端项目开发脚手架，其特点如下：

* 使用angular1（angular@1.6.2）作为项目主框架，并包含jQuery（jquery@3.1.1）、bootstrap库作为辅助工具；
* 使用bootstrap-sass（bootstrap-sass@3.3.7）作为css框架，可以覆盖bootstrap-sass/assets/stylesheets/bootstrap/_variables.scss文件中的默认配置，从而自定义样式；
* 整合angular-ui-router作为路由管理；
* 整合font-awesome开源图标库；；=
* 使用webpack2（webpack@2.2.1）前端模块化开发工具作为项目自动化构建与开发工具；
* 使用webpack-dev-server作为开发过程工具（热替换HMR）；
* 分别使用webpack.config.js与webpack.production.config.js两个webpack配置文件作为项目在开发环境中的配置和项目在生产环境中的配置。

使用方法：

1. fork再clone，或直接clone，或直接下载；
2. 打开文件所在目录，打开命令行工具至项目所在目录`npm install`安装依赖（国内的同志建议将npm的模块下载域名配置为淘宝镜像域名，或安装cnpm，**node-sass在国内只能使用cnpm下载安装，否则报错。建议先`cnpm install node-sass --save-dev`，再`npm install`**）；
3. 命令行运行`npm start`，开启开发模式，命令行运行`npm run build`，生成生产环境部署文件。

开始你的angular1模块化开发之旅:)
