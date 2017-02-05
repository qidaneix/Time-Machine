---
title: 代码风格管理神器——EditorConfig
date: 2017-02-05 21:07:51
tags:
 - EditorConfig
 - .editorconfig
 - 代码风格管理
categories:
 技术周边
---

# EditorConfig

&emsp;&emsp;代码风格（格式或规范）管理是程序员的一个老大难的问题。

&emsp;&emsp;首先，程序员往往会对不同的语言设定不同的代码规范，所谓代码规范，是指对所编写的代码的一些可设置项，
例如代码的字符集（*GBK*&*UTF-8*）、缩进字符类型（*TAB*&*Space*）、缩进字符个数（2个&4个）等等进行一定的约束。
这些代码规范也许不是语言强制规定的（python对代码缩进有强制规定），但是对于所编写代码的可读性和可维护性非常重要。
其次，每个程序员都要面对不止一种代码，例如前端程序员，使用HTML、css、JavaScript三种语言都是家常便饭，更不用说typescript、scss等语言包装，
而每一种语言又都有其合适的代码规范，HTML嵌套较多，若4空格缩进会使单行过长，所以适合2空格缩进，JavaScript则习惯于4空格缩进，这样代码层次清晰，可读性强。
但是，在同一编辑器中切换不同的代码格式是一件比较麻烦的事，有些编辑可以为不同语言设置不同格式（例如webstrom、sublime），有些则不行（VS Code？我半天没有找到）。
而且，不同的编辑器对代码格式的设置位置也不相同，若程序员需要切换工作环境（使用不同的编辑器或者在不同电脑上的相同编辑器），
要寻找这些编辑器的代码格式设置位置并进行重新设置就会变得非常麻烦。不同语言的代码风格和不同的编辑器让代码规范设定变成一个难题，为了解决这个难题，
**EditorConfig**应运而生。

![EditorConfig](http://editorconfig.org/logo.png)

&emsp;&emsp;EditorConfig就是上面那只戴着眼镜的老鼠。它对代码格式配置的思想很简单：不再是以某一种语言或者莫一种编辑器为单位，而是以项目工程为单位进行格式配置。
程序员在工程根目录下创建名为*.editorconfig*的文件，作为这个工程中所编写的所有代码的格式配置文件，*.editorconfig*的文件拥有统一的语法来对各种语言规范进行设置，
不同的编辑器通过自带或者安装插件的形式来支持EditorConfig的功能，支持EditorConfig功能的编辑器会自动解析*.editorconfig*文件，获取工程中各文件代码的格式设定信息，
从而进行对应设置，程序员只需要讲工程中的各种语言的格式规范写进该*.editorconfig*文件中，即可轻松解决在多种同语言、不同编辑器的条件下，为工程配置一致的代码规范的问题。

&emsp;&emsp;下面是[EditorConfig官网](http://editorconfig.org/)主要内容的中文翻译，*版权归EditorConfig所有，侵删*。

## 什么是EditorConfig？

&emsp;&emsp;EditorConfig帮助开发者在不同的编辑器或者IDE之间设定和维护一致的代码风格。EditorConfig由一个定义了代码风格的**配置文件**和一个可以使文本编辑器读取配置
文件并将代码设置为配置文件中定义好的代码风格的**编辑器插件**组成。EditorConfig配置文件具有优秀的可读性，并可以在版本控制器（*git*、*SVN*等）的管理下运行良好。

## EditorConfig配置文件长啥样？

### 配置文件示例

&emsp;&emsp;下面是一个*.editorconfig*配置文件的示例，这个配置文件为Python和JavaScript文件设定了行尾（end-of-line）和缩进风格。

```
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
[*.{js,py}]
charset = utf-8

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

&emsp;&emsp;可以在[工程中使用的EditorConfig配置文件](https://github.com/editorconfig/editorconfig/wiki/Projects-Using-EditorConfig)
中查看在真实环境中的配置文件案例。