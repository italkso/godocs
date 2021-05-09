## 使用 KVC 间接更改对象状态



> **KVC**（Key-Value-Coding，键值编码）是一种**间接**更改对象状态的机制，其实现方法是「**使用字符串表示要更改的对象状态**」。



### 关键词

间接	元数据	自动装箱	键路径	快速运算



### 1. KVC 简介

如何**直接**更改对象的状态呢？一般有以下几种方法：

- 常规方法调用：直接调用方法
- 属性语法：属性的点表示法
- 设置实例变量

那么，能不能间接改变对象的状态呢？

我们知道，OOP 的核心就是间接（indirection）技术的使用。使用Cocoa 提供的一种叫做 **KVC** 的特性，可以间接的改变对象的状态。Core Data 和 Cocoa Bindings等一些高级的 Cocoa 特性的基础机制中也都包含了 KVC。

**KVC**（Key-Value-Coding，键值编码）是一种**间接**更改对象状态的机制，其实现方法是「**使用字符串表示要更改的对象状态**」，具备**自动装箱**功能。



### 2. KVC 中的基本调用

#### 通过键检索和设置值

方法`-valueForKey` 和 `-setValue:forKey:`是 KVC 中的基本调用，它们使用单个键获取和设置值。实现方法是，KVC 首先查找 getter 和 setter 方法，如果找不到任何 getter 和 setter 方法，KVC 将直接进入对象并更改值。

假设 airplane 对象拥有 name 属性，那么访问及更改 name 属性的值的写法如下：

```objective-c
NSString *name = [airplane valueForKey:@"name"];
[airplane setValue: @"Fly2" forKey: @"name"];
[airplane setValue: [NSNumber numberWithFloat: 312.4] forKey: @"speed"];
```

`-valueForKey:`的查找顺序是：首先查找以参数命名（`-key` 或 `-isKey`）的 getter 方法，如果没有这样的 getter方法，就在对象中寻找名称格式为`_key` 或 `key` 的实例变量。`-valueForKey`在 Objective-C 运行时钟使用**元数据**打开对象并进入其中查找需要的信息，所以，即使没有 getter 方法也能获取对象的值，不需要通过对象指针来直接访问实例变量。

`-setValue:forKey:`的查找顺序类似：首先查找名称（比如-setName）的 setter 方法，然后调用并传递参数`@“Fly2”`。如果没有 setter 方法，KVC 就在类中寻找名为为`name` 或 `_name`的实例变量。

注意，编译器和 Apple 公司都以**下划线开头**的形式保存实例变量的名称。

对于 KVC， Cocoa 会**自动装箱**和开箱标量值。自动装箱指的是，当使用 `-setValue:forKey:`时，KVC 会自动将int、float、struct 等标量值放入 NSNumber 或 NSValue 中；当使用`-valueForKey`，KVC 会将标量值从这些对象中取出。



#### 键路径

通过在对象和不同的变量名称之间使用**圆点**表示**键路径**(KeyPath)，作用是在对象的网络中指定路径。使用键路径比使用一系列嵌套方法调用更容易访问到对象。键路径的深度取决于对象图（Object Graph）的复杂度。

```objective-c
[airplane setValue: [NSNumber numberWithFloat: 1022] forKeyPath: @"engine.turbo.temperature"];
NSLog(@"temperature is %@", [airplane valueForKeyPath:@"engine.turbo.temperature"]);
```

你还可以将各种运算符嵌入键路径中，以使 KVC 实现其他功能。

**整体操作**

如果你使用某个键值来访问一个 NSArray 数组，它实际上会查询数组中的每个对象，然后将查询结果打包到另一个数组中并返回给你。这样适用于通过键路径访问的位于对象中的数组。

KVC认为 对象中的 NSArray 具有「一对多」的关系。如果键路径中含有一个数组属性，则该键路径的其余部分将被发送给数组中的每个对象。

不过不能在键路径中索引数组。

**快速运算**

键路径不仅能够引用对象值，还能引用一些运算符进行运算，比如`@count`、`@sum`、`@avg`和`@distinctUnionOfObjects` 等。

注意，虽然 KVC 能够轻松处理集合类，切勿滥用。因为 KVC 需要解析字符串来计算所需答案，速度比较慢。



**批处理**

你可以使用以下两个调用批量更改对象：

`dictionaryWithValuesForKeys:`方法接收一个字符串数组，该调用获取「键的名称」并对每个键使用`valuesForKey:`方法，然后为键字符串和刚刚获取的值创建一个字典。

#### 重写

可以通过重写定制个别行为（corner-case）。

重写 nil 值可以提供逻辑上有意义的值。如果得到一个意料之外的键，总将调用超类方法。

处理未定义的键：`-valueForUndefinedKey:`和`-setValueForUndefinedKey:`方法。



**Reference**

[1] Learn Objective-C on the Mac For OS X and iOS（2nd Edition）