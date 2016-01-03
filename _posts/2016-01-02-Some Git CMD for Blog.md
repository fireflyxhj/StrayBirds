---
layout: post
title: Commit changes to github with git in Ubuntu
category: Technology
comments: true
---



#**Commit changes to github with git in Ubuntu**
*** 
##**本地仓库初始化**

安装git工具

git init会在当前目录下建立git仓库
***
##**配置github账户**

git config --global user.name "Elon Xu"

git config --global user.email "fireflyxhj@163.com"

git config --global credential.helper cache

git clone http://github.com/fireflyxhj/blog
***
##**添加文件**

git remote -v

git status

git add <文件>

git commit -m <文件>

git push -v origin gh-pages
##**参考链接**

[*Git commit to github*](http://www.cnblogs.com/fanyong/p/3424501.html)

[*github account*](https://github.com/fireflyxhj/blog)

[*github搭建的blog*](http://fireflyxhj.github.io/blog/)


