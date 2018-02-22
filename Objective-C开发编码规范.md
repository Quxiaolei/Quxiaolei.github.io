# Objective-C开发编码规范

<!-- TOC -->

- [Objective-C开发编码规范](#objective-c开发编码规范)
    - [命名](#命名)
    - [代码结构](#代码结构)
    - [代码格式](#代码格式)
    - [方法](#方法)
    - [相关方法/函数的使用](#相关方法函数的使用)
    - [注释](#注释)

<!-- /TOC -->

## 命名

- 语言(单词)书写要规范,变量命名尽量包含足够多的相关描述性信息.
(相关资料:[Class Names Must Be Unique](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/DefiningClasses/DefiningClasses.html#//apple_ref/doc/uid/TP40011210-CH3-SW12))

```objectivec
UIColor *myColor = [UIColor whiteColor];
//UIColor *myColour = [UIColor whiteColor];
```

- 图片等资源文件的命名,要符合语义和使用场景.并且要放在对应的资源文件夹中.
- 常量/类名等需要遵守驼峰命名法:所有单词首字母大写,并在前加上类名前缀.

常量是容易重复被使用和无需通过查找和代替就能快速修改值.

常量应该使用`static`来声明而不是使用`#define`,除非显式地使用宏.

```objectivec
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";
static CGFloat const RWTImageThumbnailHeight = 50.0;
```

还可以使用`extern`变量来声明常量:

```objectivec
//.h文件
extern NSString *const kMarketIdAppleAppStore;
extern CGFloat const RWTImageThumbnailHeight;
//.m文件
NSString *const kMarketIdAppleAppStore = @"AppleAppStore";
CGFloat const RWTImageThumbnailHeight = 44.0f;
```

- 类别的定义应该它的功能性相关.类别中的方法和属性应该以app或者组织名为前缀.(有效的避免了无意间重写了已存在的方法)

```objectivec
@interface NSString (NSStringEncodingDetection)
@interface NSArray (NYTAccessors)
- (id)nyt_objectOrNilAtIndex:(NSUInteger)index;
@end
```

类似的,推荐使用`枚举类型`(`NS_ENUM()`),固定基本类型来进行类型检查和代码补全.

```objectivec
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

```objectivec
typedef NS_OPTIONS(NSUInteger, NYTAdCategory) {
    NYTAdCategoryAutos      = 1 << 0,
    NYTAdCategoryJobs       = 1 << 1,
    NYTAdCategoryRealState  = 1 << 2,
    NYTAdCategoryTechnology = 1 << 3
};
```

- 尽量保证头文件中的属性使用`readonly`修饰.避免属性值在外部被修改.

```objectivec
@interface MyClass: NSObject
//默认为strong
@property (nonatomic) NSString *headline;
//定义一个public的getter方法
@property (nonatomic, readonly) Type propertyName;
//使用BOOL属性时,自定义getter方法
@property (nonatomic, assign, getter = isSomething) BOOL something;
@end
// @interface MyClass : NSObject {
//     NSString *headline;
// }

@interface MyClass ()
// Private Access
//定义一个private的setter方法
@property (nonatomic, strong, readwrite) Type propertyName;
@end
@implementation MyClass
@end
```

- 应尽量避免使用`back`属性(`_variable`,变量名前面有下划线)直接访问`实例变量`.

除了在初始化方法(`init`,`initWithCoder:`等),`dealloc`方法和自定义的`setter`,`getter`方法.(使用实例变量来避免`setter`,`getter`方法的潜在副作用.参考:[Don’t Use Accessor Methods in Initializer Methods and dealloc](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6))

```objectivec
//init方法返回值为:instancetype,而不是id
- (instancetype)init {
    self = [super init];
    if (self) {
        _count = [[NSNumber alloc] initWithInteger:0];
        // 不能使用`setter`,`getter`方法
        // self.count = [[NSNumber alloc] initWithInteger:0];
    }
    return self;
}
- (void)dealloc {
  // 释放资源,停止线程等操作.
  // 资源的释放顺序应该按照它们的初始化顺序或者定义的顺序.
  [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```

- 为了有助于代码代码,所有属性都应该显式地列出来.属性特性的顺序应该是`storage`,`atomicity`,与在Interface Builder连接UI元素时自动生成代码一致.

使用`__strong`,`__weak`,`__unsafe_unretained`, `__autoreleasing`等限定符时,要保证限定符在星号和变量之间.(eg:`NSString * __weak text`)

(相关资料:[ARC Introduces New Lifetime Qualifiers](https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011226-CH1-SW4))

```objectivec
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (copy, nonatomic) NSString *tutorialName;
```

参考资料:[Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE)

## 代码结构

在类似的的功能函数分组和protocol/delegate实现中使用`#pragma mark -`来分类方法.

参考:

```objectivec
#pragma mark - Lifecycle

//init方法返回值为:instancetype,而不是id
- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

## 代码格式

- 使用空格而不是制表符 Tab:Xcode默认设置为4个空格
- 方法的大括号和其他大括号(`if`/`else`/`switch`/`while`等)的使用:总是在同一行语句打开,在新一行中关闭.

```objectivec
if (user.isHappy) {
    //Do something
} else {
    //Do something else
}
```

```objectivec
- (void)writeVideoFrameWithData:(NSData *)frameData timeStamp:(int)timeStamp {
...
}
```

- 在方法类型(`-`/`+` 符号)之后有一个空格,第一个大括号`{`的位置在函数所在行的末尾，同样应该有一个空格.

`and`的作为连接,只有方法参数为多个时才使用.
函数名很长时,可以使用换行,但是参数一定要对齐.函数调用同理.

```objectivec
//init方法返回值为:instancetype,而不是id
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
//- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
```

- 在`case`语句中,当一个`case`语句包含多行代码时,应该加上大括号.

使用布尔值时,需要特别注意:

objectivec使用`YES`和`NO`表示布尔值.正确的使用方法:

```objectivec
// nil检查
if (someObject) {}
if (![anotherObject boolValue]) {}
#pragma mark 错误的使用方法
// if (someObject == nil) {}
// if ([anotherObject boolValue] == NO) {}
// if (isAwesome == YES) {} // Never do this.
// if (isAwesome == true) {} // Never do this.
```

为了使得代码便于阅读,避免书写错误,尽量把判断条件表达式中判断的值倒写.

```objectivec
if (2 == indexPath.section) {
}
```

此处需要引入`guard`/`黄金路径`的概念:

当使用条件语句编码时,左手边的代码应该是"golden"或"happy"路径.也就是要尽量避免if语句的嵌套.

```objectivec
- (void)someMethod {
  if (![someOther boolValue]) {
    return;
  }
  //Do something important
}
```

不应该是:

```objectivec
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

- 文件资源的导入使用`#import`.`modules`的导入使用`@import`.

```objectivec
// Frameworks
@import QuartzCore;

// Models
#import "NYTUser.h"

// Views
#import "NYTButton.h"
#import "NYTUserView.h"
```

避免过多的使用`#import`,建议使用`@class`代替依赖导入.(参考资料:[Don’t #import in Header Files Unnecessarily](https://ashfurrow.com/blog/structuring-modern-objectivec/#dont-import-in-header-files-unnecessarily))

```objectivec
@class MyOtherClass;
@interface MyClass : NSObject
@property (nonatomic, strong) MyOtherClass property;
@end

// #import "MyOtherClass.h"
// @interface MyClass : NSObject
// @property (nonatomic, strong) MyOtherClass property;
// @end

#import "MyOtherClass.h"
@implementation MyClass
@end
```

## 方法

头文件中应该只保存`public`接口方法和属性,`private`/`protected`的方法应该在实现文件中定义.

方法命名时尽量不要以`set`,`get`开头,重写`setter`,`getter`方法除外.

- 代理方法的一个属性应该是发送消息的对象(比如:`tableView`).

```objectivec
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath;
```

- `setter`,`getter`方法

```objectivec
- (void)setFoo:(NSString *)aFoo {
  [_foo autorelease];
  //字符串的赋值或者传递时保证其值以copy的形式存在,避免在不知情的情况下修改string值
  _foo = [aFoo copy];
}
````

- 初始化方法

避免使用`new`方法创建对象或者在子类中重写此方法,应该使用`alloc`和`init`方法实例化对象.

`init`方法:返回类型应该使用`instancetype`而不是`id`.

```objectivec
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```

当类构造方法被使用时,它应该返回类型是`instancetype`而不是`id`.

```objectivec
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```

- 单例的创建

单例对象应该使用线程安全模式来创建共享实例.

```objectivec
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

## 相关方法/函数的使用

应用程序应该避免直接访问和修改保存在`CGRect`数据结构中的数据.

```objectivec
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
// CGFloat x = frame.origin.x;
// CGFloat y = frame.origin.y;
// CGFloat width = frame.size.width;
// CGFloat height = frame.size.height;
// CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

尽量使用点语法调用`setter`,`getter`方法.

```objectivec
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
// [view setBackgroundColor:[UIColor orangeColor]];
// UIApplication.sharedApplication.delegate;
```

`NSStringFromClass()`,`NSClassFromString()`等的使用.

`CGFLOAT_MIN`宏定义的使用.

## 注释

避免过多的注释使用,建议使用代码的自解释实现.
以下情况需要格外注意并作出相应注释:

1. 产品需求临时变更:需要额外标注时间,任务,目的,其他tips等

    `2017年06月18日21:07:13 @XX 需求由A变更为B`

    另:需求变更需要邮件/任务等备份存档.
2. 需求/bug临时解决方案/TODO

官方编码规范:

[Apple Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)

[Google objectivec Style Guide](https://google-styleguide.googlecode.com/svn/trunk/objcguide.xml?showone=Line_Length#Line_Length)

[GitHub objectivec Style Guide
](https://github.com/github/objectivec-style-guide)

[Wikimedia objectivec Style Guide
](https://www.mediawiki.org/wiki/Wikimedia_Apps/Team/iOS/ObjectiveCStyleGuide)

[Introduction to Coding Guidelines for Cocoa](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)

[objectivec编码规范[译]](http://www.jianshu.com/p/8b76814b3663)

[objectivec开发编码规范](http://www.cocoachina.com/ios/20150508/11780.html)

[objectivec编码规范：26个方面解决iOS开发问题](http://www.imooc.com/article/1216)
