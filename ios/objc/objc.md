## Objective-C





### 布尔类型

布尔类型是可以存储真值和假值的变量类型，可以用作变量、函数的参数和返回值等的类型。Objective-C提供的布尔类型（BOOL）具有 YES 和 NO 两个值。Objective-C 中的 BOOL 是一种对带符号的字符类型（signed char）的类型定义（typedef），通过 #define 指令把 YES 定义为 1，把 NO 定义为 0。因此，可以直接与 NO 比较，但不能把 BOOL 值和 YES 值直接进行比较。



### Methods

```objective-c
//	Define methods - class methods
+ (type)doSomething;

//	Define dethods - instance methods
- (type)doSomething;
- (type)doSomethingWithA: (type)a;
- (type)dosomethingWithA: (type)a b:(type)b;

//	Implementate methods
- (type)doSomethingWithA: (type)a b:(type)b{
    //	do something with a and b
    return returnValue;
}

//	Calling a method after an Object has Created
ClassName *myObject = [[ClassName alloc] init];

[myObject doSomething];
[myObject doSomethingWithA:a];
[myObject dosomethingWithA:a b:b];
```

### Variables

```objective-c
//	Use int,float,double,BOOL, ClassName * or id to substitute type
type myVariables;
```

| Variable Types   | Description                                                  | Initialize |
| ---------------- | ------------------------------------------------------------ | ---------- |
| `int`            |                                                              | `0`        |
| `float` `double` |                                                              | `0.0`      |
| `BOOL`           | `YES`, `NO`                                                  | `NO`       |
| `ClassName *`    | `NSArray *`, `NSString*`...                                  | `nil`      |
| `id`             | **id** is a pointer to an instance of a class, and hold reference to any object | `nil`      |



### Initializer

```objective-c
- (id)initWithParameter: (type) parameter {
    if ((self = [super init])) {
        _propertyName = parameter;
    }
    return self;
}
```

### Category

```c
typedef struct objc_category *Category;
```



### NSString

```objective-c
NSString *firstString = @"apple";
NSString *secondString = @"banana";
NSString *joinedString = [NSSring stringWithFormat: @"%@, %@ !"];
NSlog("%@", joinedString);

NSString *price = @"24.99";
float anotherString = [anotherString floatValue];
```

### NSArray

```objective-c
NSMutableArray *myArray = [@[firstString, secondString] mutableCopy];
[myAaray addObject:@"grape"];
NSLog(@"%d items!", [myAaray count]);
for (NSString *fruit in myArray) {
    NSLog(@"Fruit: %@", fruit)
}

NSString *grape = myArray[2];
```





## Block



### 3. OOP

OOP is short for **Object-Oriented Programming**. The core concept of OOP is **indirection**. Variables, file name and command line arguments are three example of indirection.

- **class**
  - class、superclass / parentclass、subclass / childclass
- **object**
- **instance**
- **message**
- **method**
- **method selectors **: the name of a method at runtime
- **method dispatcher**
- **interface**
- **implementation**

```c
// Class
typedef struct objc_class *Class;

//	Ivar ( instance variable )
typedef struct objc_ivar *Ivar;

//	Method
typedef struct objc_method *Method;

//	SEL
// You must use the value returned from sel_registerName or the Objective-C 	       
// compiler directive @selector() When using selectors.
typedef struct objc_selector *SEL;
SEL sel_registerName(const char *str);

//	objc_method_description

struct objc_method_description {
    ...
};

//	objc_property_t
typedef struct objc_property *objc_property_t;

//	objc_super
struct objc_super {
    ...
};

//	id
typedef struct objc_object {
    ...
} id;
```

NSObject is the root class of most Objective-C class hierarchies.

### Inheritence

### Composition

### Category

### Protocal



## 内存管理（Memory Management）

### 内存管理（Memory Management）

Objective-C's memory management system is called **reference counting**. You need to keep track of your references, and the runtime does the actual freeing of memory for you. 

In simplest terms, you *alloc* an object, maybe *retain* it at some point, then send one *release* for each alloc/retain you sent. So if you used alloc once and then retain once, you need to release twice.

If you create an object using the manual *`alloc`* style, you need to *`release`* the object later. 

```objective-c
// string1 will be released automatically
NSString* string1 = [NSString string];

// must release this when done
NSString* string2 = [[NSString alloc] init];
[string2 release];
```

#### Init

```objective-c
- (id) init
{
    if ( self = [super init] )
    {
        [self setCaption:@"Default Caption"];
        [self setPhotographer:@"Default Photographer"];
    }
    return self;
}
```



#### Dealloc

```objective-c
- (void) dealloc
{
    [caption release];
    [photographer release];
    [super dealloc];
}
```

Objective-C是面向对象的C语言，C 和 C++语句均可出现在Objective-C代码中，可以调用 C 函数，也可通过 C++对象访问方法。

理解 C语言的内存模型（memory model），有助于理解Objective-C的内存模型和引用计数（reference count）机制的工作原理。指针是 C语言的精髓，也是理解内存模型的关键。Objective-C 中的指针是用来指示对象的，即所有对象都是指针的形式。

对栈和堆的内存管理不同。分配在栈上用于保存变量的内存则会在其栈帧弹出时自动清理。而对象所占内存总是分配在堆空间（heap space），分配在堆中的内存必须直接管理。Objective-C运行期环境将堆内存管理抽象成一套名为引用计数的内存管理架构。



### Pointer and Memory Model in C



### Heap Space



### Reference Count



## 框架（Framework）

框架（Framework）是一种把头文件、库、图片、声音等内容聚集在一个独立单元中的集合体。每个框架都是一个重要的技术集合，通常包含数十个甚至上百个头文件。通过在主头文件中使用`#import`，就可以访问框架内的所有功能。

- Cocoa 由 Foundation 和 ApplicationKit（AppKit）组成
- Cocoa Touch  Foundation 和 UIKit 组成
- 支持型框架(如 CoreGrapgics、Core Animation 和 Core Image 等)。

### Foundation 框架

Foundation 框架处理的是用户界面之下的那些层（Layer）的特性，如数据结构和通信机制。

通过查看 Headers目录，就可以知道 Foundation 框包含了哪些头文件。使用`#import <Foundation/Foundation.h>`来包含主头文件，就能获得整个集合。Xcode 会使用预编译头文件（一种经过压缩的、摘要形式的头文件）来加快读取速度。

**NS 前缀**来源于 Cocoa 的前身 NextStep，表明函数来自 Cocoa 工具包，用于避免名称冲突。由于 Cocoa 已经占用了 NS 前缀，所以自定义的任何变量和函数前不能使用 NS 前缀，以免混淆。



- **NSRange**

```objc
//	NSRange
typedef struct _NSRange
{
    unsigned int location;
    unsigned int length;
} NSRange;

//	Create New NSRange
NSRange range = NSMakeRange(42, 5 );
```

- **CGPoint, CGSize, CGRect**

```objc
struct CGPoint 
{
    float x;
    float y;
};//CGPoint

struct CGSize
{
  float width;
  float height;
};//CGSize

struct CGRect
{
    CGPoint origin;
    CGSize size;
};//CGRect
```

- **NSString**

```objective-c
+ (id) stringWithFormat: (NSString *) format, ...;

- (NSUInteger) length;

- (BOOL) isEqualToString: (NSString *) aString;

/*Case Insensitive*/
- (NSComparisonResult) compare: ( NSString *) aString;	

/*
 *options: NSCaseInsensitiveSearch, NSLiteralSearch, NSNumericSearch (using bitwise-   	*OR)
 */
- (NSComparisonResult) compare: ( NSString *) aString options: (NSStringCompareOptions) mask;	

- (BOOL) hasPrefix: (NSString *) aString;
- (BOOL) hasSuffix: (NSString *) aString;
- (NSRange) rangeOfString: (NSString *) aString;
```

```objective-c
/*Example*/
NSString *distance;
distance = [NSString stringWithFormat:@"Your distance is %d m, %d cm", 2,6];

NSUInteger length = [distance length];
```

- **NSMutableString**

```objective-c
// Defenition
+ (id) stringWithCapacity: (NSUInteger) capacity;
- (void) appendString: (NSString *) aString;
- (void) appendFormat: (NSString *) foramt, ...;
- (void) deleteCharactersInRange: (NSRange) aRange;

/*Example*/
NSMutableString *string = [NSMutableString stringWithCapacity: 64];
[string appendString:@"Hi,"];
[string appendFormat:@"nice to meet you,%d", 42];

```

- **NSArray, NSMutableArray, NSEnumerator 和 Fast Enumeration**

```objective-c
//	Create a new array (the latter is recommended)
NSArray *array = [NSArray aarayWithObjects:@"a",@"b",@"c",nil];
NSArray *array = @[@"a",@"b",@"c"]];
id *myObject = array[2];

//	Methods
- (NSUInteger)count;
- (id)objectAtIndex: (NSUInteger)index;
- componentsSeparatedByString
- componentsJoinedByString
    
//	Create a new mutable array using the following class method
+ (id)arrayWithCapacity: (NSUInteger) numItems;
- (void) addObject: (id) object;
- (void) removeObjectAtIndex: (NSUInteger) index;
    
//	Example
NSString *string = @"apple,pineapple,orange,peal,peach";
NSArray *chunks = [string componentSeperatedByString:@","];
string = [chunks componentJoinedByString:@"-"];
```

可以使用 `index`, `NSEnumerator` , `Fast Enumeration` 和 `Block` 遍历一个数组。

```objective-c
//	NSEnumerator
- (NSEnumerator *)objectEnumerator;
- NSEnumerator *firstEnumerator = [array objectEnumerator];
- NSEnumerator *secondEnumerator = [array reverseObjectEnumerator];
- (id) nextObject;

//	Fast Enumeration (non-concurrent)
for (NSString *string in array)
{
    NSLog(@"The element of array %@", string);
}

//	Block (concurrent)
- (void)enumerateObjectsUsingBlock:(void (^)(id obj, NSUInteger idx, BOOL *stop))block;
[aaray enumerateObjectsUsingBlock:^(NSString *string, NSUInteger index, BOOL *stop){
    NSLog(@"The element of array %@", string);
}];
```

- **NSDictionary**

```objective-c
+ (id) dictionaryWithObjectsAndKeys: (id)firstObject, ...);
- (id) objectForKey: (id) aKey;
+ (id) dictionaryWithCapacity: (NSUInteger) numItems;
- (void) setObjectForKey:(id)anObject forKey:(id)aKey;
- (void) removeObjectForKey: (id)aKey;
```

- **NSNumber**

```objective-c
// Boxing - Create a new NSNumber object - 1
+ (NSNumber *) numberWithInt: (int) value;
+ (NSNumber *) numberWithFloat: (float) value;
+ (NSNumber *) numberWithBool: (BOOL) value;
+ (NSNumber *) numberWithChar: (char) value;

// Boxing - Create a new NSNumber object Using literal - 2
NSNumber *number = @23;
number = @23ul;
number = @23ll;
number = @1.2345f;
number = @1.2345;
number = @NO;
number = @"H";

// Unboxing
- (int) intValue;
```

```c
//	iOS, macOS, Mac Catalyst, tvOS
typedef long NSInteger;	
typedef unsigned long NSUInteger;

//	watchOS
typedef int NSInteger;	
typedef unsigned int NSUInteger;
```

- **NSNull 和 NSValue**

```objective-c
+ (NSNull *) null;
```

- **BOOL**

```c
typedef bool BOOL;	//Defines YES as 1, NO as 0
typedef signed char BOOL;	//	


// True on all platforms
- (bool)value {
    return 256;
}

if ([self value]) doStuff();
```

`BOOL` 实际上是 `char`类型，和 C/C++中布尔类型不一样。



### AppKit 框架



### UIKit 框架



## KVC



保存、检索数据，分解数据，使用 KVC 间接处理数据



## KVO