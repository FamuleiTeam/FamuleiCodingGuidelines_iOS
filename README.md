伐木累iOS代码规范v1.0





VC的结构（推荐）





命名

  推荐使用长的、描述性的方法和变量名。尽量写全，

推荐:

    UILabel *nameLabel;  

不推荐:

    UILabel *nameLbl;



常量

常量应该以驼峰法命名，并以相关类名作为前缀。

推荐:

    static const NSTimeInterval FMLSignInViewControllerFadeOutAnimationDuration = 0.4;

不推荐:

    static const NSTimeInterval fadeOutTime = 0.4;



方法

方法名与方法类型 (-/+ 符号)之间应该以空格间隔。方法段之间也应该以空格间隔（以符合 Apple 风格）。参数前应该总是有一个描述性的关键词。

尽可能少用 "and" 这个词。它不应该用来阐明有多个参数，比如下面的 initWithWidth:height: 这个例子：

推荐:

    - (void)setExampleText:(NSString *)text image:(UIImage *)image;
    - (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
    - (id)viewWithTag:(NSInteger)tag;
    - (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;

不推荐:

    - (void)setT:(NSString *)text i:(UIImage *)image;
    - (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
    - (id)taggedView:(NSInteger)tag;
    - (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
    - (instancetype)initWith:(int)width and:(int)height;  



类

类名应该以大写字母作为前缀

推荐:

    FMLXXXViewController

不推荐:

    XXXViewController



属性

属性应该尽可能描述性地命名，避免缩写，并且是小写字母开头的驼峰命名。



属性定义

推荐按照下面的格式来定义属性

    @property (nonatomic, readwrite, copy) NSString *name;

属性的参数应该按照下面的顺序排列： 原子性，读写 和 内存管理。

习惯上修改某个属性的修饰符时，一般从属性名从右向左搜索需要修动的修饰符。最可能从最右边开始修改这些属性的修饰符，根据经验这些修饰符被修改的可能性从高到底应为：内存管理 > 读写权限 >原子操作

必须使用 nonatomic，除非特别需要的情况。在iOS中，atomic带来的锁特别影响性能。

Block必须使用 copy （block 最早在栈里面创建，使用 copy让 block 拷贝到堆里面去）



点符号

当使用 setter getter 方法的时候尽量使用点符号。应该总是用点符号来访问以及设置属性。

例子:

    view.backgroundColor = [UIColor orangeColor];
    [UIApplication sharedApplication].delegate;

不要这样:

    [view setBackgroundColor:[UIColor orangeColor]];
    UIApplication.sharedApplication.delegate;



方法

参数断言

你的方法可能要求一些参数来满足特定的条件（比如不能为nil），在这种情况下最好使用 NSParameterAssert() 来断言条件是否成立或是抛出一个异常。

私有方法

永远不要在你的私有方法前加上 _ 前缀。这个前缀是 Apple 保留的。



初始化

init方法返回instancetype,不推荐返回id



单例写法

推荐

    + (instancetype)sharedInstance
    {
       static id sharedInstance = nil;
       static dispatch_once_t onceToken = 0;
       dispatch_once(&onceToken, ^{
          sharedInstance = [[self alloc] init];
       });
       return sharedInstance;
    }



Categories

 category 方法和属性前加上自己的小写前缀以及下划线，比如- (id)fml_myCategoryMethod



NSNotification

当你定义你自己的 NSNotification 的时候你应该把你的通知的名字定义为一个字符串常量，就像你暴露给其他类的其他字符串常量一样。你应该在公开的接口文件中将其声明为 extern 的， 并且在对应的实现文件里面定义。

因为你在头文件中暴露了符号，所以你应该按照统一的命名空间前缀法则，用类名前缀作为这个通知名字的前缀。

同时，用一个 Did/Will 这样的动词以及用 "Notifications" 后缀来命名这个通知也是一个好的实践。

    // Foo.h
    extern NSString * const FMLFooDidBecomeBarNotification
    
    // Foo.m
    NSString * const FMLFooDidBecomeBarNotification = @"FMLFooDidBecomeBarNotification";



Pragma

Pragma Mark

#pragma mark -  是一个在类内部组织代码并且帮助你分组方法实现的好办法。




