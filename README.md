# 智艺创想 Objective-C 代码风格编写指南

本指南用于简要描述智艺创想约定的代码编写指南,基于 [Apple’s Cocoa Coding Guidelines](https://developer.apple.com) 和 [raywenderlich.com](http://www.raywenderlich.com) 编写.暂时不包含 C++ 和 C 语言相关代码规范.

## 概述

编写该指南的目的是为了保持我们开发过程中代码风格一致,更利于不同的开发人员阅读和维护代码.

该指南和苹果官方指南有较大差距,很多决定都是为了减少屏幕占用空间,易于阅读增加代码的自解释性.

该指南目前还在修订版本中,会不定期更新维护,以最新发布版本为准.

## 作者

该指南由[lipyoung](https://github.com/LipYoung)编写.[smelloftime](https://github.com/smelloftime)共同修订.

特别感谢 [raywenderlich.com](http://www.raywenderlich.com).

## 补充

以下是苹果官方文档编码指南.如果对于本编码规范有任何不全面或者争议的部分,可以在 Xcode 的官方文档中搜索 ` Coding Guidelines for Cocoa` 进行查阅.

或者你也可以查阅以下在线文档:

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)


## Table of Contents

* [语言](#语言)
* [缩写](#缩写)
* [代码分组](#代码分组)
* [代码注释](#代码注释)
* [空格与换行](#空格与换行)
* [注释](#注释)
* [命名](#命名)
* [方法](#方法)
* [变量](#变量)
* [属性特征](#属性特征)
* [点语法](#点语法)
* [字面值](#字面值)
* [常量](#常量)
* [枚举](#枚举)
* [case](#case)
* [私有属性](#私有属性)
* [布尔值](#布尔值)
* [条件语句](#条件语句)
* [初始化](#初始化)
* [类构造方法](#类构造方法)
* [CGRect](#CGRect)
* [最佳路径](#最佳路径)
* [错误处理](#错误处理)
* [单例模式](#单例模式)
* [换行符](#换行符)
* [Xcod工程](#Xcod工程)
* [OOP](#OOP)


## 语言

必须使用英语进行编码!注释可以使用中文.

**最佳:**
```objc
// This is sample code.
UIColor *myColor = [UIColor whiteColor];
```

**不建议:**
```objc
UIColor *wodeYanse = [UIColor whiteColor];
```
## 缩写

当使用缩写时,**必须**使用网络上能轻易查询到的缩写.如果统一达成共识的缩写必须注明在工程的 `README.md` 文件下.

```shell
统一缩写表

ViewControl -> VC
```


## 代码分组

使用 `// MARK: - ` 来对代码进行分组.遵循以下结构:

```objc

// MARK: - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

// MARK: - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

// MARK: - IBActions

- (IBAction)submitData:(id)sender {}

// MARK: - Public

- (void)publicMethod {}

// MARK: - Private

- (void)privateMethod {}

// MARK: - Protocol conformance
// MARK: - UITextFieldDelegate
// MARK: - UITableViewDataSource
// MARK: - UITableViewDelegate

// MARK: - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

// MARK: - NSObject

- (NSString *)description {}
```

## 代码注释

编写注释时使用最新的Xcode 8支持的注释.按照不同的情况分为以下几种

``` objc
区分代码段落
// MARK: - 
// MARK:

提示修复内容
// FIXME: 

未完成功能
// TODO:
```
没有特殊说明,不准随意使用 `#warning` 注释!

头文件注释规定如下:

``` objeC
//
//  AppDelegate.h ( 类名称 )
//  YiHe ( 工程名称 )
//
//  Created by lip on 16/11/2. ( 作者 )
//  Copyright © 2016年 ZhiYiCX. All rights reserved. ( 版权 )
//  应用代理类 ( 类简述 )
//  负责和应用层级相关功能交互 ( 类概述 )
// .... ( 详细设计思路 )
```


## 空格与换行

* 缩进使用 4 个空格,确保在 XCode 中进行了设置.
* 方法大括号和其他大括号(if/else/switch/while 等.)总是在同一行语句打开但在新行中关闭.

**最佳:**
```objc
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```

**不建议:**
```objc
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

* 在方法之间应该有且只有一行,这样有利于在视觉上更清晰和更易于组织.在方法内的空白部分应该分离功能,但通常都抽离出来成为一个新方法.
* 优先使用 auto-synthesis 但如果有必要 @synthesize 和 @dynamic应该在实现中每个都声明新的一行
* 应该避免以冒号对齐的方式来调用方法,虽然有时方法签名可能有3个以上的冒号和冒号对齐会使代码更加易读,但是 Xcode 的对齐方式令代码块难以辨认,所以**不允许**这样做.

**最佳:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**不建议:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

## 注释

当需要注释时,注释应该用来解释这段特殊代码为什么要这样做.任何被使用的注释都必须保持最新或被删除.

接口必须拥有详细的注释.对接口作出充分的说明.

一般都避免对私有方法注释,因为代码尽可能做到自解释.

应该避免对每段代码进行注释,只有端出现断断续续的几行代码时才需要注释.

## 命名

该部分内容取自 [Apple’s Cocoa Coding Guidelines](https://developer.apple.com).可在 Xcode 的官方文档中搜索 ` Coding Guidelines for Cocoa` 进行扩展阅读.

编写尽量长的,描述清晰的方法和变量名是最好的做法.

**最佳:**

```objc
UIButton *settingsButton;
```

**不建议:**

```objc
UIButton *setBut;
```

常量应该使用驼峰式命名规则,所有的单词首字母大写和加上与类名有关的前缀.

四个字符的前缀 `ZYCX` 是可以被使用的.并且应该用在类和常量命名时.


**最佳:**

```objc
static NSTimeInterval const ZYCXTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**不建议:**

```objc
static NSTimeInterval const fadetime = 1.7;
```

属性也是使用驼峰式,但首单词的首字母小写,对属性使用 auto-synthesis 而不是手动编写 @synthesize 语句.

**最佳:**

```objc
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

**不建议:**

```objc
id varnm;
```

### 下划线

当使用属性时,实例变量应该使用 `self.` 来访问和改变.这就意味着所有属性将会视觉效果相同,因为它们前面都有 `self.`.

但有一个特例:在初始化方法里,实例变量(例如,_variableName)应该直接被使用来避免getters/setters潜在的副作用.

局部变量不应该包含下划线.

## 方法

在方法签名中，应该在方法类型(-/+ 符号)之后有一个空格。在方法各个段之间应该也有一个空格(符合Apple的风格)。在参数之前应该包含一个具有描述性的关键字来描述参数。

"and"这个词的用法应该保留。它不应该用于多个参数来说明，就像 `initWithWidth:height` 以下这个例子：

**最佳:**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**不建议:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // 决定允许这样写!
- (instancetype)init:(int)width :(int)height;  // 决定允许这样写!
```

## 变量

变量命名时应该尽量具有描述性.除了在 `for()` 循环内,尽量避免单个字母命名.

星号表示变量是指针。正常情况下: `NSString *text` 正确,而不是使用 `NSString* text` 或者使用 `NSString * text`.

尽量使用[私有属性](#私有属性)来替代实例化变量的使用.虽然使用实例化变量也是行之有效的,但是为了代码的一致性,更建议使用[私有属性](#私有属性).

通过使用'back'属性(_variable，变量名前面有下划线)直接访问实例变量应该尽量避免，除了在初始化方法(init, initWithCoder:, 等…)，dealloc 方法和自定义的setters和getters.

**最佳:**

```objc
@interface ZYCXTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**不建议:**

```objc
@interface ZYCXTutorial : NSObject {
  NSString *tutorialName;
}
```


## 属性特征

所有属性特性应该显式地列出来，有助于阅读代码。属性特性的顺序应该是storage、atomicity，与在Interface Builder连接UI元素时自动生成代码一致。

**最佳:**

```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**不建议:**

```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

NSString等拥有可变子类的类应该使用copy 而不是 strong的属性特性。
为什么？即使你声明一个NSString的属性，有人可能传入一个NSMutableString的实例，然后在你没有注意的情况下修改它。

**最佳:**

```objc
@property (copy, nonatomic) NSString *tutorialName;
```

**不建议:**

```objc
@property (strong, nonatomic) NSString *tutorialName;
```

## 点语法

点语法是一种很方便封装访问方法调用的方式。当你使用点语法时，通过使用getter或setter方法，属性仍然被访问或修改。

为了代码的统一和简洁,在修改和访问属性时,除非有充值的理由否则**必须**使用点语法.`[]`符号更偏向于用在其他地方

**最佳:**
```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**不建议:**
```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## 字面值

NSString, NSDictionary, NSArray, 和 NSNumber的字面值应该在创建这些类的不可变实例时被使用.

**最佳:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**不建议:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

## 常量

常量是容易重复被使用和无需通过查找和代替就能快速修改值。常量应该使用 `static` 来声明而不是使用 `#define`.

**最佳:**

```objc
static NSString * const ZYCXAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const ZYCXImageThumbnailHeight = 50.0;
```

**不建议:**

```objc
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```

## 枚举

当使用enum时，使用新的固定基本类型规格，因为它有更强的类型检查和代码补全。现在 SDK 有一个宏 `NS_ENUM()` 来帮助和鼓励你使用固定的基本类型

**例如:**

```objc
typedef NS_ENUM(NSInteger, ZYCXLeftMenuTopItemType) {
  ZYCXLeftMenuTopItemMain, ///< 这是一条注释
  ZYCXLeftMenuTopItemShows,
  ZYCXLeftMenuTopItemSchedule
};
```

你也可以显式地赋值.

```objc
typedef NS_ENUM(NSInteger, ZYCXGlobalConstants) {
  ZYCXPinSizeMin = 1,
  ZYCXPinSizeMax = 5,
  ZYCXPinCountMin = 100,
  ZYCXPinCountMax = 500,
};
```

除非编写使用 C语言编写 `Core Foundation` 相关框架.否则避免使用旧的枚举方式.

**不建议:**

```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```


## Case

在编写 Case 语句时,除非含有多行代码,否则不建议加上括号.

```objc
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}

```

当相同的代码被多个 cases 使用时,需要使用下穿式语法(fall-through).下穿式语法指的是在 case 最后一处 `break`语句,这样就允许执行流程跳转执行下一个 case 的值.为了代码更佳清晰,一个下穿式语法需要注释

```objc
switch (condition) {
  case 1:
    // 下穿执行 **  fall-through! **
  case 2:
    // code executed for values 1 and 2
    break;
  default: 
    // ...
    break;
}

```

当在switch使用枚举类型时，'default'可以删除.

```objc
ZYCXLeftMenuTopItemType menuType = ZYCXLeftMenuTopItemMain;

switch (menuType) {
  case ZYCXLeftMenuTopItemMain:
    // ...
    break;
  case ZYCXLeftMenuTopItemShows:
    // ...
    break;
  case ZYCXLeftMenuTopItemSchedule:
    // ...
    break;
}
```


## 私有属性

私有属性应该在实现文件(.m)的类扩展中声明.命名时不需要增加类似 `private`的关键字.

**例如:**

```objc
@interface ZYCXDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

## 布尔值

`Objective-C`必须使用 `YES` 和 `NO`。因为 `true` 和 `false` 应该只在 `CoreFoundation`，C 或 C++ 代码使用。

既然nil解析成NO，所以没有必要在条件语句比较。也不要拿某样东西直接与YES比较，因为YES被定义为 1 但一个 BOOL 有可能被设置为 8 bits .所以为了在阅读不同文件时,视觉上一致.

**最佳:**

```objc
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**不建议:**

```objc
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

设置 `BOOL` 属性是,需要参考一贯的 `get` 访问器名称.例如:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

## 条件语句

条件语句**必须**使用大括号圆,哪怕有的时候不需要大括号(如只编写一行代码的条件语句时).

**最佳:**
```objc
if (!error) {
  return success;
}
```

**不建议:**
```objc
if (!error)
  return success;
```

或者

```objc
if (!error) return success;
```

### 三目运算符


当需要提高代码的清晰性和简洁性时，三目运算符`?:`才会使用。单个条件求值时,也可以考虑使用它.

多个条件求值时，如果使用`if` 条件语句或重构成实例变量时，代码会更加易读时,就避免编写过于复杂和冗余的三目运算语句。为了可读性,也**不允许**编写嵌套的三木运算语句.

一般来说，最好使用三目运算符是在根据条件来赋值时.

**最佳:**
```objc
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = isHorizontal ? x : y;
```

**不建议:**
```objc
result = a > b ? x = c > d ? c : d : y;
```

## 初始化

初始化必须按照官方的代码模板.

```objc
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```


## 类构造方法

当类构造方法被使用时，它应该返回类型是instancetype而不是id。这样确保编译器正确地推断结果类型。

```objc
@interface Airplane
+ (instancetype)airplaneWithType:(ZYCXAirplaneType)type;
@end
```


## CGRect

当访问 CGRect 里的 `x, y, width, height` 时，应该使用CGGeometry函数而不是直接通过结构体来访问.

**最佳:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**不建议:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

## 最佳路径

当使用条件语句编码时,正确逻辑处理的代码写在左侧,也就是说永远**避免**编写嵌套的 `if` 语句.当有多个条件判断语句时,也是如此

**最佳:**

```objc
- (void)someMethod {
  if (![someOther boolValue]) {
	return;
  }

  //Do something important
}
```

**不建议:**

```objc
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

**例如:**

```swift
if let object1= optional1 {
  // do something with object1 here
  if let object2 = optional2 {
     if let object3 = optional3 {
       // do something with objects 1,2,3
     }
   }
}

// 转换为

if let object1 = optional1 && object2 = optional2 {
}

```

**例如:**

```swift

if let object1= optional1 {
  if let object2 = optional2 {
     if let object3 = optional3 {
        // important code is nested deep inside here...
     }
   }
} else {
  // handle missing values
}

// 转换为

if optional1 == nil || optional2 == nil || optional3 == nil {
  // handle missing values
  return;
}

let object1 = optional1!
let object2 = optional2!
let object3 = optional3!

// important code is aligned with the left

```

## 错误处理

当方法通过引用来返回一个错误参数，判断返回值而不是错误变量。

**最佳:**
```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

**不建议:**
```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```

Some of Apple’s APIs write garbage values to the error parameter (if non-NULL) in successful cases, so switching on the error can cause false negatives (and subsequently crash).


## 单例模式

单例对象应该使用线程安全模式来创建共享实例。

```objc
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

这可以防止某些崩溃.


## 换行符

换行符是一个很重要的主题，因为它的风格指南主要为了打印和网上的可读性。

**例如:**

```objc
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
```

一行很长的代码应该分成两行,下一行用两个空格隔开.

```objc
self.productsRequest = [[SKProductsRequest alloc] 
  initWithProductIdentifiers:productIdentifiers];
```


## Xcod工程

### 工程目录

在工程中物理文件应该与Xcode工程文件保持同步!任何文件都必须按照类型或者功能来进行分组,使代码更佳清晰.

**例如:**

``` shell
.
├── Podfile ( pod 三方包说明 )
├── Podfile.lock ( pod 版本锁 )
├── README.md ( 工程说明 )
├── YiHe ( 主工程 )
│   ├── AppDelegate.h
│   ├── AppDelegate.m
│   ├── Assets.xcassets ( 图片素材 )
│   ├── Base.lproj ( 启动图目录 )
│   │   └── LaunchScreen.storyboard
│   ├── CXFoundation ( 工程基础文件夹 )
│   │   └── Tools ( 工程基础工具包 )
│   ├── Category ( 类别 )
│   ├── Class ( 主要的类 )
│   │   ├── HomePage ( 功能模块名称 )
│   │   │   ├── Models ( 功能模块数据文件夹 )
│   │   │   ├── ViewController.h ( 功能模块控制器 )
│   │   │   ├── ViewController.m
│   │   │   └── Views ( 功能模块视图文件夹)
│   │   └── Public ( 公用的类 )
│   ├── Info.plist ( 应用配置信息 )
│   └── main.m ( 系统文件 )
└── YiHeTests ( 测试文件 )
          ├── Info.plist ( 应用配置信息 )
          ├── Info.plist
          ├── MainTest ( 功能模块测试文件 )
          │   ├── Units ( 单元测试文件夹 )
          │   └── Case ( 测试用例 )
          └── Public ( 公用的测试 )
```

### PCH文件

工程禁止使用 `.pch`文件,因为会建议编译效率和性能.

### 三方库

为了避免冲突,所以建议尽量使用cocoapods来使用和管理三方,同时**不允许**直接修改pod管理的三方库源文件的源代码.

## OOP

在编写代码的过程中应遵循面向对象设计思路,对代码进解耦.为督促大家采用面向对象编程.控制器中的代码行数不应该超过500行.每个对象依照复杂程度不同,属性成员数量不应该超过10个.

当遇到代码无法满足该标准时,对代码进行拆分和重构,达到解耦和易于测试的目的.
