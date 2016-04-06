伐木累iOS代码规范



ViewController的布局

布局与风格并不影响执行速度、内存使用量等方面程序的布局。编排出色的代码会带来视觉上和思维上的愉悦，这是非程序员的人不能感受到的。如果你做的是合作项目,这块内容还是蛮重要的,尽量统一大家的风格。

好布局有什么用

- 准确表现代码的逻辑结构
- 改善可读性
- 经得起修改
  布局技术

- 分组
      #pragma mark - Init methods		///初始化方法
      #pragma mark - View lifeCycle   ///生命周期
      #pragma mark - Common methods   ///自定义方法
      #pragma mark - Action methods	/// UI响应事件
      #pragma mark - UITableViewDelegate /datasource Methods ///delegate
      #pragma mark - Getter/Setter	///getter
  
- 空格
      eg:     //属性
      @property (nonatomic, readonly, strong) NSDictionary *statuCodeToMessageDictionary;
       1. property 后留空格
       2. 修饰符“,”后留空格
       3. 修饰符“()”后留空格
       4. 所有变量的类名后留空格
       5. 类型标识符和尖括号内的协议名之间不能有任何空格
       6. 属性的参数应该按照下面的顺序排列： 原子性->读写->内存管理 
      (这些修饰符被修改的可能性从高到底应为：内存管理 > 读写权限 >原子操作)
       7. 如无特别情况，使用nonatomic修饰，atomic带来的互斥锁特别影响性能。
      
      eg:     //方法
      - (void)setAnimatingWithStateOfTask:(NSURLSessionTask *)task;
      1.方法返回值前留空格
      2.方法返回值后不留空格
      3.左括号和方法名在同行并有空格隔开
      4.多个参数的方法换行并以冒号对齐
      
      
- 换行
      eg：//method  推荐写法（不完全为了美观）
      - (BOOL)validateResponse:(NSHTTPURLResponse *)response
                          data:(NSData *)data
                         error:(NSError *__autoreleasing *)error;
         //不推荐写法（参数很多的情况，可读性很差）
      - (BOOL)validateResponse:(NSHTTPURLResponse *)response data:(NSData *)data error:(NSError *__autoreleasing *)error;
      
      
- 缩进
        eg： //常用的字符串(推荐写法)
      
         NSString *string = @"Rose";
      
            //不推荐写法
        NSString*string=@"Rose";
      
      
- 对齐
         eg: //create UILabel  推荐写法 （组织结构明了，易于修改，可维护性强）
           UILabel *testLabel = [[UILabel alloc]init];
      
           testLabel.frame = CGRectMake(50, 50, 50, 50);
           testLabel.text = @"The cute Rose";
           testLabel.textColor = [UIColor yellowColor];
      
           [self.view addSubview:testLabel];
      
               //不推荐 （凌乱, 臃肿，简直不想看）
          UILabel*testLabel=[[UILabel alloc]init];
        testLabel.frame=CGRectMake(50, 50, 50, 50);
          testLabel.text=@"The cute Rose";
       testLabel.textColor=[UIColor yellowColor];
              [self.view addSubview:testLabel];
      
      
- 其他考虑
  1. 段落之间使用空行
  2. 单语句代码块的格式要前后统一
  3. 对于复杂的表达式，将条件分隔放在多行上





命名

 推荐使用长的、描述性的方法和变量名。尽量写全，该名字要完全，准确地描述出该变量所代表的事物。通常对变量的描述 就是最佳的变量名。这种名字容易阅读，因为其中并不包含晦涩的缩写， 同时也有歧义，因为它是对该事物的完整描述，不会和其他事物混淆， 因此也容易记忆。

     * 针对不同视图控制器，在末尾添加后缀，eg：
     * UIViewController  后缀添加“ViewController”
     * UIView 后缀添加“View”
     * UIButton 后缀添加“Button"
     * UILabel 后缀添加“Label"

推荐:

    UILabel *nameLabel;  

不推荐:

    UILabel *nameLbl;

  注意 model这层为了清晰，我们以FMLM开头为前缀，M代表为Model





常量

宏和常量不强制，放在统一的地方，宏k开头，常量量是模块+名字

推荐:

    static const NSTimeInterval FMLSignInViewControllerFadeOutAnimationDuration = 0.4;
    #define kApplication @"xxx"

不推荐:

    static const NSTimeInterval fadeOutTime = 0.4;
    #define Application @"xxx"



方法

- 描述方法所做的事情
- 避免使用无意义、模糊或者标书不清的动词
- 对返回值有所描述
- 不要传递过多参数（建议限制大约在7个以内）

推荐

    - (void)selectItemAtIndexPath:(nullable NSIndexPath *)indexPath
                    animated:(BOOL)animated scrollPosition:
                    (UICollectionViewScrollPosition)scrollPosition;
    
      - (void)appendPartWithInputStream:(NSInputStream *)inputStream
                        name:(NSString *)name
                    fileName:(NSString *)fileName
                      length:(int64_t)length
                    mimeType:(NSString *)mimeType; 
    
      - (NSMutableURLRequest *)requestWithMethod:(NSString *)method
                    URLString:(NSString *)URLString
                  parameters:(id)parameters
                        error:(NSError * __autoreleasing *)error;



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



准确使用对仗词

       add/remove               begin/end           insert/delete
       increment/decrement      show/hide           create/destory
       open/close               lock/unlock         source/target
       first/last               max/min             start/stop
       get/put                  next/previous       up/down
       get/set                  old/new             high/low



类

类名应该以大写字母作为前缀

推荐:

    FMLXXXViewController

不推荐:

    XXXViewController



属性

属性应该尽可能描述性地命名，避免缩写，并且是小写字母开头的驼峰命名。

尽量不要用实例变量如_name,使用属性替代

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

协议

如果类名为FMLSignViewController那么，协议用来返回用户点击事件，那么协议最好使用

    (void)signViewController:(FMLSignViewController *)signViewController didClickxxx:(NSString *)parameter

原始数据类型

推荐使用NSUInteger这类Apple定义的数据类型.

如 

    int -> NSInteger
    unsigned -> NSUInteger
    float -> CGFloat
    动画时间 -> NSTimeInterval

枚举

- 枚举常量
  1. 使用枚举来定义一组相关的整数常量
  2. 枚举常量与其typedef命名遵循函数命名规则。
- 延伸（非命名规则）
  C语言风格的enum定义枚举类型
      enum {
           UIViewAnimationTransitionNone,  
           UIViewAnimationTransitionFlipFromLeft,  
           UIViewAnimationTransitionFlipFromRight,  
           UIViewAnimationTransitionCurlUp,  
           UIViewAnimationTransitionCurlDown,  
      
       }   UIViewAnimationTransition; 
      
      //位移操作枚举定义  
      enum {  
           UIViewAutoresizingNone                 = 0,  
           UIViewAutoresizingFlexibleLeftMargin   = 1 << 0,  
           UIViewAutoresizingFlexibleWidth        = 1 << 1,  
           UIViewAutoresizingFlexibleRightMargin  = 1 << 2,  
           UIViewAutoresizingFlexibleTopMargin    = 1 << 3,  
           UIViewAutoresizingFlexibleHeight       = 1 << 4,  
           UIViewAutoresizingFlexibleBottomMargin = 1 << 5  
      };   
      typedef NSUInteger UIViewAutoresizing;
      
      

枚举值一般是4个字节的int值，在64位系统上是8个字节。iOS6以后苹果引入了两个宏来重新定义这两个枚举类型，将enum定义和typedef合二为一，并且采用不同的宏来从代码角度来区分。 NS_OPTIONS一般用来定义位移相关操作的枚举值。

通用情况，推荐使用NSENUM。NSOPTIONS一般用来定义具有位移操作或特点的情况。例如：

        typedef NS_ENUM(NSInteger, UIViewAnimationTransition) {  
            UIViewAnimationTransitionNone,//默认从0开始  
            UIViewAnimationTransitionFlipFromLeft,  
            UIViewAnimationTransitionFlipFromRight,  
            UIViewAnimationTransitionCurlUp,  
            UIViewAnimationTransitionCurlDown,  
        };  
    
        typedef NS_OPTIONS(NSUInteger, UIViewAutoresizing) {  
            UIViewAutoresizingNone                 = 0,  
            UIViewAutoresizingFlexibleLeftMargin   = 1 << 0,  
            UIViewAutoresizingFlexibleWidth        = 1 << 1,  
            UIViewAutoresizingFlexibleRightMargin  = 1 << 2,  
            UIViewAutoresizingFlexibleTopMargin    = 1 << 3,  
            UIViewAutoresizingFlexibleHeight       = 1 << 4,  
            UIViewAutoresizingFlexibleBottomMargin = 1 << 5  
        }; 
    
    



注释

对于精心编写的代码而言，注释不过是美丽衣裳上的小饰物而已。注释的种类：

            重复代码
            解释代码
            代码标记
            概述代码
            代码意图说明
    
    

注释单行或多行

- 该行代码太复杂，因此需要注释
- 该行语句出过错，留个标记
- 不要对单行代码做行尾注释
- 注释的缩进要与相应代码保持一致
- 每行注释至少用一个空行隔开
        行尾注释用于数据声明
        避免用行尾注释存放维护注记 （记录修改或者错误编号）
        用行尾注释标记块尾
      
      

注释控制结构

- 应在每个if、case、循环或者代码段前面加上注释
- 应在每个控制结构后加上注释
- 注释赢靠近其说明的代码
- 在声明参数处注释这些参数
      eg：
       /**
        基本地址URL,接口特殊性需要其他baseURL，可以覆盖此方法 默认为空
      
        @return 基本地址的URL
        */ 
      - (NSString *)baseURL;
      








