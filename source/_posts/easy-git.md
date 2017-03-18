---
title: git及github简单使用（以上传教学课件为例）
date: 2017-02-20 11:39:42
tags:
 - git
 - 代码版本维护
 - github
 - 代码托管平台
categories:
 技术周边
---

**教两个小朋友使用git进行代码版本维护以及github进行代码托管**

# 本地git库配置

1. 新建文件夹，用于存放课件
![step-1](http://oiml7svqr.bkt.clouddn.com/step-1.png)
2. 打开命令行运行窗口（cmd/shell/git均可）
![step-2](http://oiml7svqr.bkt.clouddn.com/step-2.png)
3. 在命令行内运行`cd 路径`命令使命令行至文件夹所在路径
![step-3](http://oiml7svqr.bkt.clouddn.com/step-3.png)
4. 运行命令`git init`初始化git，将文件夹由git负责版本管理
![step-4](http://oiml7svqr.bkt.clouddn.com/step-4.png)
5. 将课件移动到文件夹内
![step-22](http://oiml7svqr.bkt.clouddn.com/step-22.png)
6. 运行命令`git add *`及`git commit -m '第一次提交'`，本地git库配置完成
![step-5](http://oiml7svqr.bkt.clouddn.com/step-5.png)

# 新建github库

7. 打开github，登录
![step-6](http://oiml7svqr.bkt.clouddn.com/step-6.png)
8. 点击头像，点击“your profile”
![step-7](http://oiml7svqr.bkt.clouddn.com/step-7.png)
9. 点击组织
![step-8](http://oiml7svqr.bkt.clouddn.com/step-8.png)
10. 点击“new”，新建库
![step-9](http://oiml7svqr.bkt.clouddn.com/step-9.png)
11. 在新建库界面填写相关信息（库名建议与文件夹名同名），点击“Create repository”
![step-10](http://oiml7svqr.bkt.clouddn.com/step-10.png)
12. 页面跳转到库界面，点击“add teams and collaborators”
![step-11](http://oiml7svqr.bkt.clouddn.com/step-11.png)
13. 点击添加team,选择我们的组，使我们的组成员可以看到库
![step-12](http://oiml7svqr.bkt.clouddn.com/step-12.png)
14. 修改一下权限，使我们的组成员可以维护（可以执行clone，commit等操作）库，github库配置完成
![step-13](http://oiml7svqr.bkt.clouddn.com/step-13.png)

# 本地git库与托管平台github库关联

15. 回到‘code’界面，复制刚才新建的github库的https地址
![step-14](http://oiml7svqr.bkt.clouddn.com/step-14.png)
16. 回到命令行，运行命令`git remote add origin https://github.com/webend-learner/ES3ES5ES6-learn.git`，注意要改成自己的建的github库地址，完成本地库与托管平台github库的关联
![step-15](http://oiml7svqr.bkt.clouddn.com/step-15.png)
17. 运行命令`git push -u origin master`，输入github账户及密码（可能会出现此步骤），将本地内容推送到托管平台
![step-16](http://oiml7svqr.bkt.clouddn.com/step-16.png)
18. 刷新github新建库的界面，可以看到本地的内容已经提交到托管平台了
![step-17](http://oiml7svqr.bkt.clouddn.com/step-17.png)
19. 一般都会给库新建一个README.md文件作为库的说明页面，在本地新建README.md文件写入(这里写你自己想写的内容)：
![step-19](http://oiml7svqr.bkt.clouddn.com/step-19.png)
![step-18](http://oiml7svqr.bkt.clouddn.com/step-18.png)
20. 执行`git add *`，`git commit -m '提交README.md'`，`git push -u origin master`三个命令，完成将README.md提交到托管平台
![step-20](http://oiml7svqr.bkt.clouddn.com/step-20.png)
21. 刷新github库界面，可以看到界面底部已经有介绍内容
![step-21](http://oiml7svqr.bkt.clouddn.com/step-21.png)
22. 之后有任何新内容需要提交，重复21步的三个命令即可，或者使用SourceTree，使用可视化工具进行相关操作。
![step-23](http://oiml7svqr.bkt.clouddn.com/step-23.png)

* * *

*附上两个git教程（侵删）：*

> * [廖雪峰的git入门教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)，用于git入门学习（已足够日常使用）
> * [git-简易指南](http://www.bootcss.com/p/git-guide/)，用于快速查询常用git指令
