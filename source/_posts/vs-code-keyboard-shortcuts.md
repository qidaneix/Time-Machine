---
title: Windows版VS Code快捷键总结
date: 2017-02-05 15:38:33
tags: 
 - Visual Studio Code
 - windows
 - 快捷键
categories:
 技术周边
---

![VS Code](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSVYw4ZYa_sFVNDU-sZ068rKGmwjlVbQnbiUA6xq4jXhN3qsKglPQ)

**Visual Studio Code**是我现在使用的最频繁的代码编辑器，下面是我翻译的[Windows版VS Code快捷键总结](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)，供大家参考，若有任何错误或问题，欢迎联系我进行改正。

# 常规
|快捷键|功能|
|---|---|
|`Ctrl+Shift+P,F1`|打开VS Code命令面板|
|`Ctrl+P`|最近打开过的文件|
|`Ctrl+Shift+N`|打开新窗口|
|`Ctrl+Shift+W`|关闭窗口|

# 文本编辑
|快捷键|功能|
|---|---|
|`Ctrl+X`|剪切该行|
|`Ctrl+C`|复制该行|
|`Alt+↑/↓`|向上/向下移动该行|
|`Shift+Alt+↑/↓`|向上/向下复制该行|
|`Ctrl+Shift+K`|删除该行|
|`Ctrl+Enter`|向下插入一行|
|`Ctrl+Shift+Enter`|向上插入一行|
|`Ctrl+Shift+\`|跳转至匹配括号|
|`Ctrl+]/[`|增加/减少缩进|
|`Home`|至该行起始位置|
|`End`|至该行结束位置|
|`Ctrl+Home`|至文件起始位置|
|`Ctrl+End`|至文件结束位置|
|`Ctrl+↑/↓`|向上/向下滚动（鼠标滚轮）|
|`Alt+PgUp/PgDown`|向上/向下整页滚动|
|`Ctrl+Shift+[`|折叠某区域|
|`Ctrl+Shift+]`|展开某区域|
|`Ctrl+K Ctrl+[`|折叠所有子区域|
|`Ctrl+K Ctrl+]`|展开所有子区域|
|`Ctrl+K Ctrl+0`|折叠所有区域|
|`Ctrl+K Ctrl+J`|展开所有区域|
|`Ctrl+K Ctrl+C`|增加该行注释|
|`Ctrl+K Ctrl+U`|删除该行注释|
|`Ctrl+/`|触发该行注释|
|`Shift+Alt+A`|触发多行注释|
|`Alt+Z`|触发一行为多行显示|

# 导航
|快捷键|功能|
|---|---|
|`Ctrl+T`|打开所有符号|
|`Ctrl+G`|（按行号）至某一行|
|`Ctrl+P`|至某一文件|
|`Ctrl+Shift+O`|至某一符号|
|`Ctrl+Shift+M`|打开问题面板|
|`F8`|跳转至下一个错误或警告位置|
|`Shift+F8`|跳转至上一个错误或警告位置|
|`Ctrl+Shift+Tab`|导航历史编辑文件|
|`Alt+←/→`|至向前/向后编辑位置|
|`Ctrl+M`|触发`Tab`移动焦点|

# 搜索和替换
|快捷键|功能|
|---|---|
|`Ctrl+F`|查找|
|`Ctrl+H`|替换|
|`F3/Shift+F3`|跳转至匹配的上一个/下一个内容|
|`Alt+Enter`|选中所有匹配的内容|
|`Ctrl+D`|光标跳转至下一匹配内容后|
|`Ctrl+K Ctrl+D`|跳转至下一个匹配内容后|
|`Alt+C/R/W`|触发大小写敏感/正则/全局文本|

# 多光标和选中
|快捷键|功能|
|---|---|
|`Alt+Click`|插入光标|
|`Ctrl+Alt+↑/↓`|向上/向下插入光标|
|`Ctrl+U`|撤销上次的光标操作|
|`Shift+Alt+I`|在所有选中行结尾插入光标|
|`Ctrl+I`|选中当前行|
|`Ctrl+Shift+L`|选中所有当前选择的事件*|
|`Ctrl+F2`|选中所有当前文本的事件*|
|`Shift+Alt+→`|扩展选中范围|
|`Shift+Alt+←`|收缩选中范围|
|`Shift+Alt+(drag mouse)`|块选中*|
|`Ctrl+Shift+Alt+(arrow key)`|块选中*|
|`Ctrl+Shift+Alt+PgUp/PgDown`|上页/下页块选中*|

# 富文本编辑
|快捷键|功能|
|---|---|
|`Ctrl+Space`|触发器建议*|
|`Ctrl+Shift+Space`|触发器参数提示*|
|`Tab`|Emmet扩展缩写|
|`Shift+Alt+F`|格式化文档|
|`Ctrl+K Ctrl+F`|格式化选中内容|
|`F12`|前往定义*|
|`Alt+F12`|窥视定义*|
|`Ctrl+K F12`|打开定义到右侧*|
|`Ctrl+.`|快速修复*|
|`Shift+F12`|显示参考|
|`F2`|重命名符号*|
|`Ctrl+Shift+./,`|用上一个/下一个值替换|
|`Ctrl+K Ctrl+X`|修剪结尾空格|
|`Ctrl+K M`|改变文件语言|

# 编辑器管理
|快捷键|功能|
|---|---|
|`Ctrl+F4 Ctrl+W`|关闭编辑器|
|`Ctrl+K F`|关闭文件夹|
|`Ctrl+\`|分离编辑器|
|`Ctrl+1/2/3`|切换至第一、第二、第三个编辑器组|
|`Ctrl+K Ctrl+←/→`|切换至上一个/下一个编辑器组|
|`Ctrl+Shift+PgUp/PgDown`|向左/右移动编辑器|
|`Ctrl+K ←/→`|移动活动状态的编辑器组|

# 文件管理
|快捷键|功能|
|---|---|
|`Ctrl+N`|创建新文件|
|`Ctrl+O`|打开文件|
|`Ctrl+S`|保存|
|`Ctrl+Shift+S`|另存为|
|`Ctrl+K S`|保存所有文件|
|`Ctrl+F4`|关闭文件|
|`Ctrl+K Ctrl+W`|关闭所有文件|
|`Ctrl+Shift+T`|重新打开已关闭的编辑器|
|`Ctrl+K Enter`|保持开启|
|`Ctrl+Tab`|打开下一个编辑器|
|`Ctrl+Shift+Tab`|打开上一个编辑器|
|`Ctrl+K P`|复制活动状态文件的文件路径|
|`Ctrl+K R`|在资源管理器中展示活动状态的文件|
|`Ctrl+K O`|在新的窗口中展示活动状态的文件|

# 展示
|快捷键|功能|
|---|---|
|`F11`|触发全屏|
|`Shift+Alt+1`|触发编辑器布局|
|`Ctrl+=/-`|放大/缩小编辑器界面|
|`Ctrl+B`|触发侧边栏显示|
|`Ctrl+Shift+E`|展示侧边栏资源管理器界面|
|`Ctrl+Shift+F`|展示侧边栏搜索界面|
|`Ctrl+Shift+G`|展示侧边栏Git界面|
|`Ctrl+Shift+D`|展示侧边栏调试界面|
|`Ctrl+Shift+X`|展示侧边栏拓展插件界面|
|`Ctrl+Shift+H`|打开侧边栏搜索界面的文件内容替换功能|
|`Ctrl+Shift+J`|触发详细搜索|
|`Ctrl+Shift+C`|打开新的命令行终端|
|`Ctrl+Shift+U`|打开输出面板|
|`Ctrl+Shift+V`|触发Markdown预览|
|`Ctrl+K V`|打开Markdown预览至右侧|

# 调试
|快捷键|功能|
|---|---|
|`F9`|触发断点|
|`F5`|开始/继续|
|`Shift+F5`|停止|
|`F11/Shift+F11`|跳入/跳出|
|`F10`|跳过|
|`Ctrl+K Ctrl+I`|显示悬停|

# 集成终端
|快捷键|功能|
|---|---|
|``Ctrl+` ``|打开集成终端|
|``Ctrl+Shift+` ``|打开新的集成终端|
|`Ctrl+Shift+C`|复制集成终端中的选中内容|
|`Ctrl+Shift+V`|将内容粘贴到活动的集成终端|
|`Ctrl+↑/↓`|向上/向下滚动|
|`Shift+PgUp/PgDown`|向上/向下整页滚动|
|`Ctrl+Home/End`|滚动到顶/底|


**表示存留问题的翻译*
