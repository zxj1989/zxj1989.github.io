---
layout: post
title: "Ootopress换电脑写作"
date: 2016-04-01 15:12:32 +0800
comments: true
categories: 工具使用
---

进行以下操作的前提是git仓库是按source和master分支进行管理的。
完成以下两步操作即可再另外一台电脑进行写作：

1、将博客的源文件clone到本地的octopress文件夹内

     git clone -b source https://github.com/zxj1989/zxj1989.github.io.git octopress

2、将博客文件clone到octopress的_deploy文件夹内。
   
    cd octopress
    git clone https://github.com/zxj1989/zxj1989.github.io.git 

如果是多台电脑并行写作需要更新源文件

    cd octopress
    git pull origin source 
    cd ./_deploy
    git pull origin master