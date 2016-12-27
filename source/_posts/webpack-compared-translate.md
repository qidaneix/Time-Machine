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
*这篇博文是文章[Webpack Compared](http://survivejs.com/webpack/webpack-compared/)的中文翻译*
* * *

&emsp;&emsp;如果你把Webpack放在前段发展历史的角度来看，就能更好的理解为什么Webpack是如此强大。在早些时候，我们仅需要将一些脚本连接在一起就足够了。然而，随着时间的变化，到如今，配置管理你的JavaScript代码变成了一项繁重的任务。

&emsp;&emsp;JavaScript代码的管理问题因单页面应用（single page applications，SPAs）的出现而变得愈发严峻，因为这些单页面应用往往依赖大量的大型第三方包。现在已经有了一些解决如何处理这些第三方包加载问题的办法。你可以在页面打开时将它们全部加载，你也可以在需要使用某些第三方包时将它们单独加载。有如此多的加载方式可以使用，而Webpack为多数方式提供支持。

&emsp;&emsp;Node.js和npm（Node.js package manager）的流行为前端的依赖管理提供了更多的依据。在npm流行之前，前段代码的依赖管理是一件非常困难的事。曾经有一段时间人们开发了前端特定的包管理器（bower——译者注），但npm最终胜出。如今前端的依赖管理比先前要简单容易很多，但是仍然有许多挑战需要克服。

## 任务执行工具（Task Runners）和打包工具（Bundlers）
&emsp;&emsp;在前端发展历史上，出现了很多构建工具。*Make*也许是最为有名的，并且仍然是一个可行的选择。特定的任务执行工具，比如Grunt和Gulp，是专门给前端程序员开发的工具。npm为这两个工具提供了大量插件，使得这两个工具具备强大的功能和拓展能力。

&emsp;&emsp;高水平的任务执行工具（Make,Grunt,Gulp——译者注）是非常棒开发助手。它们允许我们以跨平台的方式执行操作。但是当我们需要将各种资源连接并打包时，新的问题就出现了。这就是我们需要诸如Browserify、Brunch和Webpack等打包工具的原因。

也有一些开发工具的替代品，我列出了以下几个：
- [JSPM](http://jspm.io/)直接将包管理推送到浏览器。它依赖于System.js，System.js是一个动态模块加载器，并能使你在开发过程中完全跳过依赖绑定步骤。你可以使用它生成产品绑定。Glen Maddern在他的[视频](https://www.youtube.com/watch?t=33&v=iukBMY4apvI)中对JSPM有非常棒的详细讲解。
- [pundle](https://www.npmjs.com/package/pundle)将自己宣传为下一代的打包工具，并且对性能作为其关注重点。
- [rollup](https://www.npmjs.com/package/rollup)特别关注对ES6代码的捆绑。它的一个主要吸引点是它为人所知的*树摇动（tree shaking）*特性。它允许你根据使用情况丢弃未被使用的代码。Webpack 2在一定程度上支持树摇动。
- [AssetGraph](https://www.npmjs.com/package/assetgraph)采取了完全不同的实现，并且它建立在试验和真实的HTML语义之上，使它对[超链接分析](https://www.npmjs.com/package/hyperlink)或[结构分析](https://www.npmjs.com/package/assetviz)等任务非常有用。
- [FuseBox](https://github.com/fuse-box/fuse-box)是一个注重速度的打包工具。它使用零配置实现，目的是开箱即用。

我将详细介绍下面的主要项目。
## Make
&emsp;&emsp;Make是一个老工具，最初版本在1977年发布。即使它是一个旧工具，它与打包工具仍然相关。Make允许你为各种不同目的编写分离的任务。例如，你可能有单独的任务用于创建生产构建、压缩JavaScript代码或运行测试程序。你可以在许多其他的工具当中发现相同的思想。
&emsp;&emsp;虽然Make大部分时候用于C语言工项目，但它并非仅限于此。James Coglan详细讨论了[如何在JavaScript中使用Make](https://blog.jcoglan.com/2014/02/05/building-javascript-projects-with-make/)。参考在Jame的博文中的实现代码如下：
### Makefile
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

## Grunt
![Grunt](http://survivejs.com/webpack/images/grunt.png)
&emsp;&emsp;Grunt在Gulp之前成为主流。 尤其是它的插件架构对于其流行有巨大贡献。 但插件通常本身很复杂。 因此，当配置增长时，可能变得难以理解发生了什么。

&emsp;&emsp;下面是一个来自[Grunt文档](http://gruntjs.com/sample-gruntfile)的示例。在这个配置中，我们定义了一个linting和一个watcher任务。当watch任务运行时，它也将触发lint任务。这样，当我们运行Grunt时，如果我们编辑我们的源代码，我们将会在我们的终端实时的收到警告。
### Gruntfile.js
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

&emsp;&emsp;然而，做的太过也会产生问题。程序员可能变得很难彻底地了解Grunt内部发生了什么。 这是从Grunt吸取的构架教训。

>注意到grunt-webpack插件允许你Grunt环境下在使用Webpack。 你可以将留给繁重的任务留给Webpack。

## Gulp
![Gulp](http://survivejs.com/webpack/images/gulp.png)
&emsp;&emsp;[Gulp](http://gulpjs.com/)采取了一种不同的实现方式。使用Gulp你处理的是真实的代码，而不是依赖于每一个插件配置。Gulp建立在管道（piping）的概念之上。如果你熟悉Unix，Gulp与Unix的思路相似。有下面这些概念：
- *Sources*对应于各个文件；
- *Filters*用于对Sources执行操作（例如，转换为JavaScript）;
- *Slinks* （例如，你的构建目录）输出构建结果的位置。

&emsp;&emsp;下面提供了一个帮助你更好理解Gulp实现的*Gulpfile*的例子，来自Gulp工程的README。它被缩写为一个切口：
### Gulpfile.js
```javascript
const gulp = require('gulp');
const coffee = require('gulp-coffee');
const concat = require('gulp-concat');
const uglify = require('gulp-uglify');
const sourcemaps = require('gulp-sourcemaps');
const del = require('del');

const paths = {
  scripts: ['client/js/**/*.coffee', '!client/external/**/*.coffee']
};

// Not all tasks need to use streams.
// A gulpfile is just another node program
// and you can use all packages available on npm.
gulp.task('clean', del.bind(null, ['build']);

gulp.task('scripts', ['clean'], function() {
  // Minify and copy all JavaScript (except vendor scripts)
  // with sourcemaps all the way down.
  return gulp.src(paths.scripts)
    // Pipeline within pipeline
    .pipe(sourcemaps.init())
      .pipe(coffee())
      .pipe(uglify())
      .pipe(concat('all.min.js'))
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('build/js'));
});

// Rerun the task when a file changes.
gulp.task('watch', gulp.watch.bind(null, paths.scripts, ['scripts']));

// The default task (called when you run `gulp` from CLI).
gulp.task('default', ['watch', 'scripts']);
```
&emsp;&emsp;gulp由代码提供配置，这样，当代码出现错误时，你就可以跟踪调试它们。你可以将现有的Node.js包封装为Gulp插件等等。相比较于Grunt，你会对（配置代码）发生了什么有一个更清楚的认识。然而你还是要为了一些临时的任务写许多的样板。但这就是一些比较新的办法。

>[webpack-stream](https://www.npmjs.com/package/webpack-stream)允许你在Gulp环境中使用Webpack。
>[Fly](https://github.com/bucaran/fly)是一个和Gulp相似的工具。它依赖于ES6生成器。

## Browserify
![Browserify](http://survivejs.com/webpack/images/browserify.png)
&emsp;&emsp;如何处理JavaScript模块是个困难。在ES6之前，JavaScript语言本身实际上没有“模块”的概念。因此，当处在浏览器环境中时，我们总是感觉被困在90年代。因此，人们提出了包括[AMD](http://requirejs.org/docs/whyamd.html)在内的各种解决方案.

&emsp;&emsp;在实践当中，只有CommonJs这种解决方案在Node.js的格式中最为有用，并且让工具处理其余的工作。（CommonJS）的优点是你可以钩在npm上，避免重复早轮子。

&emsp;&emsp;Browserify是解决模块化问题的一种方案。它提供了一种将CommonJS模块捆绑在一起的方法。你可以用Gulp将它挂载。有更小的允许你跨越基本用法的转换工具。例如，[watchify](https://www.npmjs.com/package/watchify)提供了一个可以在你开发过程中生成捆绑的文件监视器。这样做会节省不少麻烦，毫无疑问是一种非常好的解决方案。

&emsp;&emsp;Browserify生态系统由很多小模块组成。Browserify以此坚持Unix的理念。 Browserify比Webpack更容易使用，事实上，它是一个很好的Webpack的替代品。

>[Splittable](https://github.com/cramforce/splittable)是一个允许代码拆分的Browserify包装器，支持ES6开箱，树摇动，等等。

## Brunch
![Brunch](http://survivejs.com/webpack/images/brunch.png)
&emsp;&emsp;与Gulp相比，Brunch运行在一个更高层次的抽象上。它使用类似于webpack的声明式方法。为了给你一个例子，从Brunch网站改编的以下配置可供参考：
```javascript
module.exports = {
  files: {
    javascripts: {
      joinTo: {
        'vendor.js': /^(?!app)/,
        'app.js': /^app/
      }
    },
    stylesheets: {
      joinTo: 'app.css'
    }
  },
  plugins: {
    babel: {
      presets: ['es2015', 'react']
    },
    postcss: {
      processors: [require('autoprefixer')]
    }
  }
};
```
&emsp;&emsp;Brunch使用类似于`brunch new`、`brunch watch --server`和`brunch build --production`这样的指令实现。它包含很多可以对功能进行扩展的开箱即用（out of box）的插件。

>这里有一个对Brunch[热模块重加载运行](https://github.com/brunch/hmr-brunch)的试验。

## JSPM
![JSPM](http://survivejs.com/webpack/images/jspm.png)
&emsp;&emsp;JSPM的使用方法与先前的工具非常不同。它自带了一个很小的CLI工具，这个CLI工具可以用于安装新的包到项目，创建一个生产捆绑等等。 它支持SystemJS插件，SystemJS插件允许您将各种格式加载到项目中。

&emsp;&emsp;鉴于JSPM仍然是一个年轻的项目，可能有粗糙的点。也就是说，如果你富于冒险精神，它可能值得一看。如你所知，在前端开发领域，工具经常发生变化，而JSPM绝对是一个重量级的竞争对手。

## Webpack
![Webpack](http://survivejs.com/webpack/images/webpack.png)
&emsp;&emsp;你可以说[Webpack](https://webpack.js.org/)采用了比Browserify更为整体的解决方案。相比较于Browserify由大量小的工具组成，Webpack提供了一个包含很多开箱即用的功能的核心。这个核心可以使用特定的*加载器（loaders）*和*插件（plugins）*进行拓展。

&emsp;&emsp;它可以控制*解析（resolves）*模块的方式，使其可以适应你的构建以匹配特定的情况，并避开那些不能完美地开箱即用的包。虽然过分依赖Webpack的解析机制并不为人所推荐，但可以提供不同的选项是一件好事。

&emsp;&emsp;Webpack将遍历（traverse）项目中的`require`和`import`语句，并生成你已定义的绑定。加载机制也适用于CSS，并且支持`@import`。还有用于特定任务的插件，例如缩小，本地化，热加载等。

&emsp;&emsp;下面是一个`require（'style-loader！css-loader！./main.css'）`加载*main.css*的内容，并通过CSS和样式加载器从右到左处理它的例子.默认情况下，结果将内联到你的JavaScript代码中，并且鉴于这样做对生产使用并不是很好，将会有一个插件将其提取为单独的文件。

&emsp;&emsp;鉴于这种声明方式将项目源码与Webpack相联系，所以最好在配置时设置加载器。下面是一个改编自9[官方webpack教程](https://webpack.js.org/get-started/)的示例配置：
### webpack.config.js
```javascript
var webpack = require('webpack');

module.exports = {
  // Where to start bundling
  entry: {
    main: './entry.js'
  },
  // Where to output
  output: {
    // Output to the same directory
    path: __dirname,
    // Capture name from the entry using a pattern.
    filename: '[name].js'
  },
  // How to resolve encountered imports
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
  // What extra processing to perform
  plugins: [
    new webpack.optimize.UglifyJsPlugin()
  ],
  // How to adjust module resolution
  resolve: {
    // This would be a good place to monkeypatch packages
    alias: { ... }
  }
};
```
&emsp;&emsp;给定的配置是用JavaScript编写的，它的可塑性很强。只要是JavaScript，Webpack就可以很好的与之配合。

&emsp;&emsp;配置模型可能使Webpack在有些时候有点不透明，因为它很难理解它在做什么。这对于更复杂的情况尤其如此。 涵盖这些是这本书(《SurviveJS - Webpack》)存在的主要原因之一。


...未完待续