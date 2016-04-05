---
layout: post
title: "UI Test初窥"
date: 2016-04-05 14:20:34 +0800
comments: true
categories: Objective-C
---

##1、关于UI Test

   UI Test是iOS9加入的一个新的UI测试框架，它可以让我们通过编写代码获取页面元素并与之进行交互，以验证用户界面元素的属性和状态。
   
##2、在已有项目中使用UI Test   
在iOS9之前，我们创建的项目默认会包含一个（工程名+Tests）的Target，该Target主要是用来做单元测试。主要做一些功能的测试。如果我们需要在已有的老项目中加入UI Test只需要完成下面两个步骤即可：

###第一步：选中Xcode左上角的Test navigator按钮，如下图
![MacDown Screenshot](http://7xsms4.com2.z0.glb.clouddn.com/step1.png)

###第二步：点击左下角“+”添加按钮，如下图
![MacDown Screenshot](http://7xsms4.com2.z0.glb.clouddn.com/step2.png)

点击New UI Test Target完成UI Test的添加，添加之后该Target会自带一个UITests类。完成以上步骤即可以开始编写测试代码，进行UI测试了。