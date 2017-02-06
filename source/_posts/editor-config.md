---
title: 代码规范管理神器——EditorConfig
date: 2017-02-05 21:07:51
tags:
 - EditorConfig
 - .editorconfig
 - 代码规范管理
categories:
 技术周边
---

&emsp;&emsp;代码规范（或称代码格式或代码风格）管理是程序员的一个老大难的问题。

&emsp;&emsp;首先，程序员往往会对不同的语言设定不同的代码规范。所谓代码规范，是指对所编写的代码的一些例如字符集（*GBK*&*UTF-8*）、缩进字符类型（*TAB*&*Space*）、缩进字符个数（2个&4个）等可设置项进行一定的约束。这些代码规范也许不是语言强制规定的（python对代码缩进有强制规定），但是对于所编写代码的可读性和可维护性非常重要。其次，每个程序员都要面对不止一种代码，例如前端程序员，使用HTML、css、JavaScript三种语言都是家常便饭，更不用说typescript、scss等语言包装。而每一种语言又都有其合适的代码规范，例如HTML嵌套较多，若4空格缩进会使单行过长，所以适合2空格缩进，JavaScript则习惯于4空格缩进，使代码层次清晰，可读性强。但是，在同一编辑器中切换不同的代码格式是一件比较麻烦的事，有些编辑可以为不同语言设置不同格式（例如webstrom、sublime），有些则不行（VS Code？我半天没有找到）。而且，不同的编辑器对代码格式的设置位置也不相同，若程序员需要切换工作环境（使用不同的编辑器或者在不同电脑上的相同编辑器），要寻找这些编辑器的代码格式设置位置并进行重新设置就会变得非常麻烦。不同语言的代码风格和不同的编辑器让代码规范设定变成一个难题，为了解决这个难题，**EditorConfig**应运而生。

![EditorConfig](http://editorconfig.org/logo.png)

&emsp;&emsp;EditorConfig就是上面那只戴着眼镜的老鼠。它对代码格式配置的思想很简单：不再是以某一种语言或者某一种编辑器为单位，而是以项目工程为单位进行格式配置。程序员在工程根目录下创建名为*.editorconfig*的文件，作为这个工程中所编写的所有代码的格式配置文件，*.editorconfig*的文件具有相对于各种编辑器而言统一的语法来对各种语言格式进行设置，不同的编辑器通过自带或者安装插件的形式来支持EditorConfig的功能，支持EditorConfig功能的编辑器会自动解析*.editorconfig*文件，获取工程中各文件代码的格式设定信息，从而进行对应设置，程序员只需要将工程中的各种语言的格式规范写进该*.editorconfig*文件中，即可轻松解决在多种同语言、不同编辑器的条件下，为工程配置一致的代码规范的问题。

&emsp;&emsp;下面是[EditorConfig官网](http://editorconfig.org/)主要内容的中文翻译，*版权归EditorConfig所有，侵删*。

# 嘛是EditorConfig？

&emsp;&emsp;EditorConfig帮助开发者在不同的编辑器或者IDE之间设定和维护一致的代码风格。EditorConfig由一个定义了代码风格的**配置文件**和一个可以使文本编辑器读取配置文件并将代码设置为配置文件中定义好的代码风格的**编辑器插件**组成。EditorConfig配置文件具有优秀的可读性，并可以在版本控制器（*git*、*SVN*等）的管理下运行良好。

# EditorConfig配置文件长啥样？

## 配置文件示例

&emsp;&emsp;下面是一个*.editorconfig*配置文件的示例，这个配置文件为Python和JavaScript文件设定了行尾（end-of-line）和缩进（indent）风格。

```
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
# 最顶层的EditorConfig文件
root = true

# Unix-style newlines with a newline ending every file
# Unix样式的换行符，换行符结束于每个文件
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
# 使用大括号扩展符号匹配多个文件
# 设置默认字符集
[*.{js,py}]
charset = utf-8

# 4 space indentation
# 4空格缩进
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
# 制表符缩进（未指定大小）
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
# 覆盖lib目录下所有的JS的缩进格式
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
# 匹配确切的package.json或.travis.yml文件
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

&emsp;&emsp;可以在wiki中[工程中使用的EditorConfig配置文件](https://github.com/editorconfig/editorconfig/wiki/Projects-Using-EditorConfig)中查看在真实环境中的配置文件案例。

## 上面这些写在配置文件中的文件搁哪呢？

&emsp;&emsp;当打开一个文件时，EditorConfig插件将会在所打开的文件的目录及其每个上级目录中寻找一个名为*.editorconfig*的文件。当到达该文件的根路径或者寻找到一个写有*root=true*的EditorConfig配置文件时，将会停止寻找*.editorconfig*文件。

&emsp;&emsp;EditorConfig配置文件将会从上至下被读取，并且最靠近的EditorConfig文件将会最晚读取。匹配上EditorConfig配置文件某一节的文件，它的内容将会按照配置文件属性设置的读取顺序被加载对应代码风格，因此，更接近这些文件的属性设置将会具有更高的优先级。

&emsp;&emsp;**对Windows系统使用者：**为了在Windows资源管理器中创建*.editorconfig*文件，你们需要创建一个名为*.editorconfig.*的文件，Windows资源管理器将会自动重命名为*.editorconfig*文件。

## 配置文件格式细节

&emsp;&emsp;EditorConfig配置文件使用与[Python ConfigParser Library](https://docs.python.org/2/library/configparser.html)使用的格式相兼容的INI格式，但在节名称中允许使用*[*和*]*符号。节名称使用[globs](https://en.wikipedia.org/wiki/Glob_(programming))文件路径格式，与[gitignore](http://manpages.ubuntu.com/manpages/intrepid/man5/gitignore.5.html#contenttoc2)所接受的格式相似。正斜杠（*/*）用作路径分隔符，八角符（*＃*）或分号（*;*）用作注释。注释应当独占一行。EditorConfig配置文件应使用UTF-8编码，使用*CRLF*或*LF*行分隔符。

&emsp;&emsp;下面将解释glob文件路径模式和EditorConfig当前支持的属性。

### 通配符模式

&emsp;&emsp;在通配符匹配的节名称中识别的特殊字符：

|类型|含义|
|---|---|
|*\**|匹配任何字符串，除了路径分隔符（*/*）|
|*\***|匹配任何字符串|
|*?*|匹配任何单个字符|
|*[name]*|匹配包含在*name*中的单个字符|
|*[!name]*|匹配不包含在*name*中的单个字符|
|*{s1,s2,s3}*|匹配任何给定的字符串（用逗号分隔）（**在EditorConfig Core 0.11.0版本之后可用**）|
|*{num1..num2}*|匹配*num1*和*num2*之间的任何整型数字，*num1*和*num2*既可以为整数也可以为负数|

&emsp;&emsp;特殊字符可以用反斜杠转义，因此不会被解释为通配符模式。

### 支持的属性

&emsp;&emsp;请注意并不是每一个插件都支持所有的属性。在wiki中有一个[完整的属性列表](https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties)

- **indent_style**：设置为“*tab*”或“*space*”以分别使用硬制表符或软制表符。
- **indent_size**：定义一个用于每个缩进级别的列数和软制表符的宽度（如果支持的话）的整数。当设置为“*tab*”时，将会使用**tab_width**的属性值（如果指定了的话）。
- **tab_width**：定义一个用于表示制表符字符的列数的整数。 这默认为**indent_size**的值，并且通常不需要指定。
- **end_of_line**：设置为*lf*，*cr*或*crlf*以控制如何表示换行符。
- **charset**：设置为*latin1*，*utf-8*，*utf-8-bom*，*utf-16be*或*utf-16le*以控制字符集。不建议使用*utf-8-bom*。
- **trim_trailing_whitespace**：设置为“*true*”以删除换行符之前的任何空格字符，“*false*”则反之。
- **insert_final_newline**：设置为“*true*”以确保文件在保存时以换行符结束，“*false*”则反之。
- **root**：应放在文件顶部并在任何节之外指定的特殊属性。设置为“*true*”可停止为当前文件查找*.editorconfig*文件。

&emsp;&emsp;当前所有属性和值都不区分大小写。它们在解析时转换为小写。通常，如果一个属性并未指定值，则将使用编辑器设置，即EditorConfig对该部分不起作用。

&emsp;&emsp;EditorConfig的某些属性不指定确定的值是可以接受的，并且常常建议如此做。例如，不需要指定**tab_width**，除非它与**indent_size**的值不同。此外，当**indent_style**设置为“*tab*”时，可能需要保留**indent_size**不指定，以便读者可以使用其首选缩进宽度查看文件。此外，如果某个属性在你的项目中未标准化（例如**end_of_line**），最好将其留空。

&emsp;&emsp;对于任何属性，“*unset*”的值是删除该属性的效果，即使之前已经设置过它。例如，将添加*indent_size=unset*语句可以使**indent_size**属性失效（并使用编辑器默认设置）。

# 不需要安装插件的编辑器（IDE）

&emsp;&emsp;下面这些编辑器原生支持EditorConfig。EditorConfig可以正常使用。

![不需要安装插件的编辑器（IDE）](http://oiml7svqr.bkt.clouddn.com/noNeed.png)

# 需要下载安装插件的编辑器（IDE）

&emsp;&emsp;为了在下面这些编辑器中使用EditorConfig，你需要安装插件。

![需要下载安装插件的编辑器（IDE）](http://oiml7svqr.bkt.clouddn.com/need.png)

# 贡献EditorConfig

## 反馈给我们

*参见[EditorConfig官网](http://editorconfig.org/)*

## 创建插件

*参见[EditorConfig官网](http://editorconfig.org/)*

# 主要贡献者

*参见[EditorConfig官网](http://editorconfig.org/)*
