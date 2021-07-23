## Objective-C 语法基础

### 1. 基本概念

#### 对象（Object）

Objective-C 通过**对象（object）**存储并传递数据，每一个 Objective-C 对象都占据着某个内存区域。

#### 消息传递（Messaging）

Objective-C 采用 **消息结构**（messaging structure），对象之间互相传递消息。消息传递是指在对象之间传递数据并执行任务的过程。方法调用（消息发送）采用方括号`[ ]`运算符。

#### 运行期环境（ Runtime）

应用程序开始运行后为其提供相关支持的代码，Runtime 提供了一些使得对象之间能够传递消息的重要函数，且包含创建类实例所用的全部逻辑。

#### 动态运行时

Objective-C 在运行时才会检查对象类型。接收一条消息后，究竟应执行什么代码，由运行期环境决定。一个类别不保证一定会回应收到的消息，如果类别收到了一个无法处理的消息，程序只会抛出异常，不会出错或崩溃。

#### 动态绑定（Dynamic Binding）

使用消息结构的语言，其运行时所执行的代码由运行环境决定，即不论是否多态，总在运行时才去查找所有执行的方法。编译器不关心接收消息的对象是什么类型，接收消息的对象问题也要在运行时处理，其过程就叫**动态绑定**。Objective-C 天生即具备动态绑定能力，因为运行期才处理消息，允许发送未知消息给对象。

#### 运行期组件（Runtime Component）

一种与开发者编写的代码相链接的动态库（dynamic library），使用 Objective-C的面向对象特性的全部数据结构及函数都在运行期组件里面。运行期组件能将开发者编写的所有代码粘合起来。



### 2. Hello World 程序

```objective-c
#import <Foundation/Foundation.h>		
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"Hello World"); 			
    }
    return 0;							
}
```

#### #import

Objective-C 使用头文件来包含结构体、符号常量和函数原型等元素的声明。使用`#import`导入头文件 ，可以保证同一个头文件仅被导入一次。
- `#import <Foundation/Foundation.h>`：导入系统头文件
- `#import "MyHeaderFile.h”`：导入项目本地的头文件

导入头文件是头文件和源文件之间建立了**依赖**关系。由于依赖关系会传递，可能导致重新编译的时间变长，也可能产生循环依赖。因此 Objective-C使用`@class`创建了一个**前向引用**，告诉编译器某个类的类名。因为编译器有时候只需要知道某个类的类名。

| 文件扩展名 | 说明                                                   |
| ---------- | ------------------------------------------------------ |
| `.h`       | 头文件（类、类型、函数和常数的声明）                   |
| `.m`       | 源代码文件（Objective-C 代码和 C代码），m 代表 message |
| `.mm`      | 源代码文件（Objective-C++代码）                        |

#### NSLog()

相比 C语言的 printf()，NSLog 添加了时间戳、日期戳和`'\n'`。`@“字符串”`中的`@`符号表明引号内的字符串应该作为 Cocoa的 NSString元素来处理，NSString 即 Cocoa 中的字符串。

```objective-c
NSLog(@"The current date and time is: %@", [NSDate date]);
```



### 3. 分离类的声明和实现

#### 接口（.h文件）

接口（interface）类为对象提供的特性描述，内容包括类的`@interface` 指令、公共 `struct` 定义、`enum`常量、`#defines` 和 `extern` 全局变量。

```objective-c
#import "AnyHeaderFile.h"	
@interface ClassName: SuperClass 
    // define public properties
    // define public methods
@end
```

#### 实现（.m文件）

实现（implementation）是使接口（interface）能够正常工作的代码，内容包括`@implementation` 指令、全局变量的定义、私有 `struct` 等。

```objective-c
//	Class Implementation(.m)
@interface ClassName ()
	//	define private properties
	//	define private methods
@end

#import "YourClassName.h"
@implementation	{
    //	define private instance variables
}
    //	implement methods
@end
```

示例（Class Interface）：

```objective-c
//	ClassName.h
#import <Cocoa/Cocoa.h>
    
@interface Photo : NSObject {
    //	Properties
    NSString* caption;
    NSString* photographer;
    
    //	Getters
    - (NSString*) caption;
    - (NSString*) photographer;
    
    //	Setters
    - (void) setCaption: (NSString*)input;
	- (void) setPhotographer: (NSString*)input;
}
@end
```

示例（Class Implementation）：

```objective-c
//	ClassName.m
#import "Photo.h"

@implementation Photo
    
//	Implementation of getters
- (NSString*) caption {
    return caption;
}

- (NSString*) photographer {
    return photographer;
}

//	Implementation of setters
- (void) setCaption: (NSString*)input
{
    [caption autorelease];
    caption = [input retain];
    //	In a garbage collected environment, you can set the new value directly.
    // caption = input;
}

- (void) setPhotographer: (NSString*)input
{
    [photographer autorelease];
    photographer = [input retain];
}
@end
```



### 4. 调用方法（Calling Methods）

```objective-c
[object method];
[object methodWithInput:input];
output = [object methodWithOutput];
output = [object methodWithInputAndOutput:input];
```

 **`id`** 类型的变量可以指向任何类型的对象。

```objective-c
id myObject = [NSString string];
NSString* myString = [NSString string];
```

Objective-C 中的 嵌套方法（**nested method** ）或函数调用:

```objective-c
[NSString stringWithFormat:[prefs format]];
```

Objective-C 中多输入参数（**Multi-Input Methods** ）的方法：

```objective-c
//	In the header
-(BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile;

//	Call this method
BOOL result = [myData writeToFile:@"/tmp/log.txt" atomically:NO];
```



### 5. 属性(Properties)

属性(Properties)用于简化对成员变量的访问，因为通过 getter 和 setter 方法访问成员变量比较麻烦。

属性自动定义了一个私有属性 `type _propertyName;`，你可以通过 `_propertyName`直接访问这个私有变量。

属性也自动定义了创建了一个 getter ( `-(type)propertyName;` ) 和 setter ( `-(void)setPropertyName: (type) name;`)。你可以使用类点语法`self.propertyName`访问 getter / setter。

```objective-c
// Define properties
@property (attribute1, attribute2) type propertyName; 

// set or get properties by dot syntax (recommended)
myObject.propertyName = a;		
b = myObject.propertyName;	

// setter or getter
[myObject setPropertyName:a];	
b = [myObject PropertyName];
```

| Attributes  | Description                        |
| ----------- | ---------------------------------- |
| `strong`    | add reference to keep object alive |
| `weak`      | object can diappear, become nil    |
| `assign`    | normal assign, no reference        |
| `copy`      | make copy on assign                |
| `atomic`    | threadsafe                         |
| `nonatomic` | non-threadsafe, better performance |
| `readwrite` | create getter and setter (default) |
| `readonly`  | create just getter                 |

Objective-C 中的所有 instance variables 默认都是私有（ private）的，所以在大多数情况下都使用**访问器 （accessors）** 读写这些变量的值。

```objective-c
//	Traditional 1.x syntax
[photo setCaption:@"Day at the Beach"];
output = [photo caption];

//	Dot syntax ( Objective-C 2.0, only be used setters and getters)
photo.caption = @"Day at the Beach";
output = photo.caption;
```



#### 创建一个对象（Creating Objects）

```objective-c
//	Create an autoreleased object
NSString* myString = [NSString string];

//	Create an object using the manual style
NSString* myString = [[NSString alloc] init];
NSNumber* value = [[NSNumber alloc] initWithFloat:1.0];
```



### 6. 类别（Categories）

A category allows you to add methods to an existing class without subclassing it or needing to know any of the details of how it's implemented. 

This is particularly useful because you can add methods to built-in objects. 

```objective-c
//	
#import <Cocoa/Cocoa.h>
            
@interface NSString (Utilities)
- (BOOL) isURL;
@end
    #import "NSString-Utilities.h"
    
//             
@implementation NSString (Utilities)

- (BOOL) isURL
{
    if ( [self hasPrefix:@"http://"] )
        return YES;
    else
        return NO;
}

@end
```



***Reference***

[Learn Objective-C](http://cocoadevcentral.com/d/learn_objectivec/) ( Cocoa Dev Central )

