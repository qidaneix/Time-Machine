---
title: 翻译《Webpack Compared》
date: 2016-12-23 00:40:10
tags: 
 - 前端模块化
 - 技术概述
 - JavaScript
categories: 
 前端技术
---

# Webpack比较
#### 这篇博文是文章[Webpack Compared](http://survivejs.com/webpack/webpack-compared/)的中文翻译
* * *

&emsp;&emsp;如果你把Webpack放在前段发展历史的角度来看，就能更好的理解为什么Webpack是如此强大。在早些时候，我们仅需要将一些脚本连接在一起就足够了。然而，随着时间的变化，到如今，配置管理你的JavaScript代码变成了一项繁重的任务。

&emsp;&emsp;JavaScript代码的管理问题因单页面应用（single page applications，SPAs）的出现而变得愈发严峻，因为这些单页面应用往往依赖大量的大型第三方包。现在已经有了一些解决如何处理这些第三方包加载问题的办法。你可以在页面打开时将它们全部加载，你也可以在需要使用某些第三方包时将它们单独加载。有如此多的加载方式可以使用，而Webpack为多数方式提供支持。

&emsp;&emsp;Node.js和npm（Node.js package manager）的流行为前端的依赖管理提供了更多的依据。在npm流行之前，前段代码的依赖管理是一件非常困难的事。曾经有一段时间人们开发了前端特定的包管理器（bower——译者注），但npm最终胜出。如今前端代买的依赖管理比先前要简单容易很多，但是仍然有许多挑战需要克服。

## 任务执行工具（Task Runners）和打包工具（Bundlers）
&emsp;&emsp;在前端发展历史上，出现了很多构建工具。*Make*也许是最为有名的，并且仍然是一个可行的选择。特定的任务执行工具，比如Grunt和Gulp，是专门给前端程序员开发的工具。npm为这两个工具提供了大量插件，使得这两个工具具备强大的功能和拓展能力。

&emsp;&emsp;高水平的任务执行工具（Make,Grunt,Gulp——译者注）是非常棒开发助手。它们允许我们以跨平台的方式执行操作。但是当我们需要将各种资源连接并打包时，新的问题就出现了。这就是我们需要诸如Browserify、Brunch和Webpack等打包工具的原因。

也有一些开发工具的替代品，我列出了以下几个：
- [JSPM](http://jspm.io/)直接将包管理推送到浏览器。它依赖于System.js，System.js是一个动态模块加载器，并能使你在开发过程中完全跳过依赖绑定步骤。你可以使用它生成产品绑定。Glen Maddern在他的[视频](https://www.youtube.com/watch?t=33&v=iukBMY4apvI)中对JSPM有非常棒的详细讲解。
- [pundle](https://www.npmjs.com/package/pundle)将自己宣传为下一代的打包工具，并且对性能作为其关注重点。
- [rollup](https://www.npmjs.com/package/rollup)特别关注对ES6代码的捆绑。它的一个主要吸引点是它为人所知的*树摇动（tree shaking）*特性。它允许你根据使用情况丢弃未被使用的代码。Webpack 2在一定程度上支持树摇动。
- [AssetGraph](https://www.npmjs.com/package/assetgraph)采取了完全不同的实现，并且它建立在试验和真实的HTML语义之上，使它对[超链接分析](https://www.npmjs.com/package/hyperlink)或[结构分析](https://www.npmjs.com/package/assetviz)等任务非常有用。
- [FuseBox](https://github.com/fuse-box/fuse-box)是一个注重速度的打包工具。它使用零配置实现，目的是开箱即用。

&emsp;&emsp;我将详细介绍下面的主要项目。
### Make
&emsp;&emsp;Make是一个老工具，最初版本在1977年发布。即使它是一个旧工具，它与打包工具仍然相关。Make允许你为各种不同目的编写分离的任务。例如，你可能有单独的任务用于创建生产构建、压缩JavaScript代码或运行测试程序。你可以在许多其他的工具当中发现相同的思想。
&emsp;&emsp;虽然Make大部分时候用于C语言工项目，但它并非仅限于此。James Coglan详细讨论了[如何在JavaScript中使用Make](https://blog.jcoglan.com/2014/02/05/building-javascript-projects-with-make/)。参考在Jame的博文中的实现代码如下：
#### Makefile
```shell
PATH  := node_modules/.bin:$(PATH)
SHELL := /bin/bash

source_files := $(wildcard lib/*.coffee)
build_files  := $(source_files:%.coffee=build/%.js)
app_bundle   := build/app.js
spec_coffee  := $(wildcard spec/*.coffee)
spec_js      := $(spec_coffee:%.coffee=build/%.js)

libraries    := vendor/jquery.js

.PHONY: all clean test

all: $(app_bundle)

build/%.js: %.coffee
    coffee -co $(dir $@) $<

$(app_bundle): $(libraries) $(build_files)
    uglifyjs -cmo $@ $^

test: $(app_bundle) $(spec_js)
    phantomjs phantom.js

clean:
    rm -rf build
```
使用Make，你可以使用Make特定的语法和终端命令建模任务。 这允许它轻松地与Webpack集成。

### Grunt
![Grunt](http://survivejs.com/webpack/images/grunt.png)
&emsp;&emsp;Grunt在Gulp之前成为主流。 尤其是它的插件架构对于其流行有巨大贡献。 但插件通常本身很复杂。 因此，当配置增长时，可能变得难以理解发生了什么。

&emsp;&emsp;下面是一个来自[Grunt文档](http://gruntjs.com/sample-gruntfile)的示例。在这个配置中，我们定义了一个linting和一个watcher任务。 当watch任务运行时，它也将触发lint任务。这样，当我们运行Grunt时，如果我们编辑我们的源代码，我们将会在我们的终端实时的收到警告。
#### Gruntfile.js
```javascript
module.exports = function(grunt) {
  grunt.initConfig({
    lint: {
      files: ['Gruntfile.js', 'src/**/*.js', 'test/**/*.js'],
      options: {
        globals: {
          jQuery: true
        }
      }
    },
    watch: {
      files: ['<%= lint.files %>'],
      tasks: ['lint']
    }
  });

  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-watch');

  grunt.registerTask('default', ['lint']);
};
```
&emsp;&emsp;实际上，为了特定目的，例如构建项目，您将有许多这样的小任务。 Grunt的能力的一个重要部分是它为你隐藏了很多的接线。

然而，做的太过也会产生问题。程序员可能变得很难彻底地了解Grunt内部发生了什么。 这是从Grunt吸取的构架教训。

>注意到grunt-webpack插件允许你Grunt环境下在使用Webpack。 你可以将留给繁重的任务留给Webpack。

### Gulp

...未完待续
