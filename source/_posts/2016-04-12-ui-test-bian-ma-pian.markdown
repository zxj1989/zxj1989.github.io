---
layout: post
title: "UI Test之:编码篇"
date: 2016-04-12 09:15:41 +0800
comments: true
categories: objective-c
---

之前我们介绍了如何在项目中加入UI Test，接下来我们将在这篇文章中介绍如何编写一个测试用例，以及一些UI Test相关测试类的常用方法等。

##初识XCTestCase
当我们创建了一个UI Test Target之后，缺省包含一个继承于XCTestCase的测试类，该类缺省实现了两个父类的方法：

1、- (void)setUp;

该类的每一个测试方法执行之前会调用此方法

2、- (void)tearDown;

该类的每一个测试方法执行完之后会调用此方法


##使用录制功能
我们写UI Test的测试用例的时候可以使用Xcode提供的录制功能进行界面交互行为的录制生成代码，具体用法如下：

第一步：选择测试文件
，点击录制按钮，如下图所示
![UI Test Record](http://7xsms4.com2.z0.glb.clouddn.com/UI%20Test%20Record_1%20.png)

第二步：完成第一步操作后，会启动APP，接下来我们开始操作，Xcode会记录并生成对应操作的测试代码

##手动编写代码

手动编写代码的话我们需要熟悉下面三个类提供的相关API

XCUIApplication

XCUIElement

XCUIElementQuery


###XCUIApplication
继承于XCUIElement，管理测试应用的启动，和关闭以及获取测试应用的运行环境等

1、- (void)launch;

启动应用

2、- (void)terminate;

关闭应用

3、@property (nonatomic, copy) NSDictionary <NSString *, NSString *> *launchEnvironment;


###XCUIElement
表示每一个UI界面元素，该类遵循XCUIElementAttributes 和XCUIElementTypeQueryProvider协议。

**XCUIElementAttributes** 该类定义了界面元素的元素属性，如：frame、enabled、selected等属性。

**XCUIElementTypeQueryProvider** 提供每一类UI元素集合的表示
如buttons表示UIButton的集合，tables表示UITableView的集合等等

1、@property (readonly) BOOL exists;

判断元素是否存在

2、@property (readonly, getter = isHittable) BOOL hittable;

判断元素是否可被点击

3、- (XCUIElementQuery *)descendantsMatchingType:(XCUIElementType)type;

获取匹配对应类型的所有子节点以及子节点的子节点的所有元素的集合

4、- (XCUIElementQuery *)childrenMatchingType:(XCUIElementType)type;

获取匹配类型的所有子节点的元素的集合

5、- (void)typeText:(NSString *)text;

为元素添加文本，改方法需要有键盘焦点

6、- (void)tap;

元素点击

###XCUIElementQuery

界面元素的集合

1、- (XCUIElement *)elementBoundByIndex:(NSUInteger)index;

获取集合内对应index的元素

2、- (XCUIElement *)elementMatchingType:(XCUIElementType)elementType identifier:(nullable NSString *)identifier;

获取对应类型和对应标识的元素

3、我们还可以以下标的形式获取对应identity的元素

XCUIApplication *app = [[XCUIApplication alloc] init];
app.buttons[@"UI Test Button”]

##运行测试用例
我们可以使用command + U快捷键运行所有测试用例，也可以点击单个测试方法前面的播放按钮进行单个用例的测试，如下图所示：

![UI Test Record Run](http://7xsms4.com2.z0.glb.clouddn.com/UI%20Test%20Record_2.png)

运行测试用例之后app自动启动，并自动完成代码对应的界面交互操作。


注意：我们在写测试方法的时候方法名必须以test开头，只有以test开头的方法测试框架才会将该方法视为一个测试用例，否则是不会执行该方法的。

##总结
当前的UI Test只能做一些简单的UI测试，对如scrollView的滑动事件支持bu不好。在测试的过程中还发现偶尔会出现判断存在且可以点击的元素，在执行tap的时候报错，找不到匹配的元素。
录制生成的代码当包含中文时，中文会被转换成被编码的串，需要手动修改。希望在未来的版本中能修复和优化这些问题，开放更多测试的API。



