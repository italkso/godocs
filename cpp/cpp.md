

## 1.C++简介

C++由 Bjarne Stroustrup 于 1979 年在贝尔实验室开始设计开发，是C语言的超集，添加了「面向对象」的特性。C++通常用于编写设备驱动程序和其他要求实时性的直接操作硬件的软件。

### C++的主要特点

- 静态类型（编译时执行类型检查）
- 编译式
- 大小写敏感、不规则且标识符内不允许出现标点字符
- 支持过程化编程
- 支持面向对象编程（封装、抽象、继承、多态）
- 支持泛型编程



### 标准的 C++的组成

- 核心语言（变量、数据类型和常量等所有构件块）

-  [C++标准库](https://en.cppreference.com/w/cpp/header)（大量用于操作文件、字符串等的函数）
  
  - 标准函数库：继承自 C 语言，如 I/O、字符串和字符处理、数学、时间、日期和本地化、动态分配、宽字符函数和其他。
  - 面向对象类库：类及其相关函数的集合
  
- 标准模板库 STL（用于操作数据结构的方法）

  

###  C++开发环境

选择合适的文本编辑器（如SublimeText）和 编译器（如GNU 的 C/C++ 编译器或 Clang 编译器）。在 macOS 上，只要安装上了Xcode， GNU 编译器就能使用了。在终端使用`g++ -v`可以查看 GCC 编译器版本。还可以指定使用特定的 C++标准编译源文件，如通过命令`g++ -g -Wall -std=c++11 helloworld.cpp`指定使用 C++11 来编译`helloworld.cpp`。

````c++
#include <iostream>					//引入头文件
using namespace std;				//使用 std 命名空间
int main(){							//程序从 main() 开始执行
    cout << "Hello,World!" <<endl	//向屏幕输出Hello,World!， endl 是 end of line 的缩写
    return 0;						//正常结束返回 0
}//helloWorld.cpp
````

编译执行C++ 程序的步骤：

- 打开一个文本编辑器，编写代码。
- 保存源文件为 `helloWorld.cpp`。
- 打开终端（命令行界面），进入源文件所在的目录。
- 键入 `g++ helloworld.cpp -o helloWorld.out`，回车编译代码。代码正确的话，终端命令提示符将会跳到下一行，并生成 `helloWorld.out` 可执行文件。
- 键入 `./helloWorld.out`运行程序。
- 屏幕上将显示 `Hello,World!`。

````bash
$ g++ helloWorld.cpp -o helloWorld.out
$ ./helloWorld.out
````

| g++常用命令选项 | 解释                                                         |
| --------------- | ------------------------------------------------------------ |
| -o              | FILE 生成指定的输出文件（用在生成可执行文件时，未指定则默认为 a.out） |
| -ansi           | 只支持 ANSI 标准的 C 语法                                    |
| -c              | 只编译并生成目标文件                                         |
| -g              | 生成调试信息（GNU 调试器可利用该信息）                       |
| -shared         | 生成共享目标文件（建立共享库）                               |
| -static         | 禁止使用共享连接                                             |
| -w              | 不生成任何警告信息                                           |
| -Wall           | 生成所有警告信息                                             |
| -E              | 只运行 C 预编译器                                            |
| -IDIRECTORY     | 指定额外的头文件搜索路径DIRECTORY                            |
| -LDIRECTORY     | 指定额外的函数库搜索路径DIRECTORY                            |
| -lLIBRARY       | 连接时搜索指定的函数库LIBRARY                                |
| -DMACRO         | 以字符串"1"定义 MACRO 宏                                     |
| -DMACRO=DEFN    | 以字符串"DEFN"定义 MACRO 宏                                  |
| -UMACRO         | 取消对 MACRO 宏的定义                                        |
| -O0             | 无优化                                                       |
| -O 或 -O1       | 优化生成代码                                                 |
| -O2             | 进一步优化                                                   |
| -O3             | 比 -O2 更进一步优化（包括 inline 函数）                      |



## 2.C++ 基本语法

### 基本语法

- **程序**

  C++中的程序定义为对象的集合（这些对象通过调用彼此的方法进行交互）。

- **分号**

  语句结束符

- **语句块**

  一组使用大括号`{ }`括起来的按逻辑连接的语句。

- **标识符**

  包含字母、数字或下划线，且不以数字开头；区分大小写；不允许出现标点符号。

- **保留字**

  即关键字，不能用作标识符名称。

- **三字符组**

  总以两个问号开头，可以出现在任何地方。三字符组是为了表示以前键盘上没有的字符。

- **空格**

  用于描述空白符、制表符、换行符和注释。空格分隔语句的各个部分，让编译器能够识别语句中的某个元素。空格还可以增强程序的可读性。

- **注释**

  `//`用于单行注释，、`/*...*/`用于多行注释。

  

### 输入输出

| I/O 库头文件 | 作用                                                         |
| ------------ | ------------------------------------------------------------ |
| `<iostream>` | **cin、cout、cerr** 和 **clog** 对象都是**iostream** 类的一个实例，分别对应于标准输入流、标准输出流、非缓冲标准错误流和缓冲标准错误流。 |
| `<fstream>`  | 为用户控制的文件处理声明服务。定义了fstream(文件流)、ofstream（输出文件流）、ifstream(输入文件流)，用于从文件读取流和向文件写入流。 |
| `<iomanip>`  | 通过参数化的流操纵器（ **setw** 、 **setprecision**）声明对执行标准化 I/O 有用的服务。 |

- 对象 **cin** 与流提取运算符 >> 结合使用，附属到键盘。

- 对象 **cout**、**cerr**和 **clog**与流插入运算符 << 结合使用，附属到显示屏。

- **cerr** 对象是非缓冲的，且每个流插入到 cerr 都会立即输出。使用 cerr 流来显示错误消息。

-  **clog** 对象是缓冲的，即每个流插入到 clog 都会先存储在缓冲区，直到缓冲填满或者缓冲区刷新时才会输出）。而其他的日志消息则使用 clog 流来输出。

   

【示例】

````c++
#include <iostream>

using namespace std;

int main()
{
	char title[50];
    double price;
 
   	cout << "Input the Title： ";
   	cin >> title >> price;		// cin对象
   	cout << "The title of the book is： " << title << endl;	// cout对象
    
    char errorString[] = "Unable to read....";
   	cerr << "Error message : " << errorString << endl;		// cerr 对象
    clog << "Error message : " << errorString << endl;		// clog对象
    
    return 0;
}

````



### 数据类型

操作系统会根据变量的数据类型，来分配内存和决定在保留内存中存储什么。

变量的大小会根据编译器和所使用的电脑而有所不同，使用 `sizeof（）` 函数可以获取各种数据类型的大小。

C++允许在 char、int、double 数据类型前放置修饰符，用来改变基本类型的含义。修饰符 unsigned 或 signed 可以作为 short 或 long 的前缀。C++允许使用速记符号来声明「无符号短整数或无符号长整数」，如 `unsigned x;`。

| 基本的C++数据类型 | 关键字  | 内存占用(字节) | 数据修饰符                    | 备注                                                         |
| ----------------- | ------- | -------------- | ----------------------------- | ------------------------------------------------------------ |
| 布尔型            | bool    | 1              |                               |                                                              |
| 字符型            | char    | 1              | unsigned或signed              | unsigned char 为 0~255，signed char 为 -128~127              |
| 整型              | int     | 4              | signed、unsigned、short、long | 使用修饰符signed、unsigned时影响数值范围，使用short、long时影响内存占用 |
| 浮点型            | float   | 4              |                               |                                                              |
| 双浮点型          | double  | 8              | long                          | long double 类型的变量占 16 个字节                           |
| 宽字符型          | wchar_t | 2 或 4         |                               | （同short int）`typedef short int wchar_t`                   |
| 无类型            | void    |                |                               | 表示类型的缺失                                               |

| 类型限定符 | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| const      | **const** 类型的对象在程序执行期间不能被修改改变。           |
| volatile   | 修饰符 **volatile** 告诉编译器不需要优化volatile声明的变量，让程序可以直接从内存中读取变量。对于一般的变量编译器会对变量进行优化，将内存中的变量值放在寄存器中以加快读写效率。 |
| restrict   | 由 **restrict** 修饰的指针是唯一一种访问它所指向的对象的方式。只有 C99 增加了新的类型限定符 restrict。 |

枚举类型：派生数据类型，由用户定义的若干枚举常量的集合。枚举指将变量的值一一列举出来，变量的值只能在列举出来的值的范围。

````C++
//枚举类型的一般形式
enum 枚举名{ 
     标识符[=整型常数], 
     标识符[=整型常数], 
... 
    标识符[=整型常数]
} 枚举变量;

//举例
enum destination { East, West, South, North } dest;
dest = North;
````



【示例】

````c++
/*
 *演示有符号整数和无符号整数之间的差别
 */
#include <iostream>

using namespace std;

int main()
{
    short int i;
    short unsigned int j;
    
    j = 50000;
    
    i = j;
    cout << i << "" << j;
    return 0;
}
````

结果：`-15536 50000`。



### 变量和常量

#### 变量

- **变量的实质**

  程序可以操作的存储区的名称

- **变量的类型**

  每个变量都有指定的类型，类型决定了变量存储的大小和布局。该范围内的值都可以存储在内存中，运算符可以应用于变量上。C++允许定义基本类型的变量，也允许定义**枚举**、**指针**、**数组**、**引用**、**结构体**和**类**等类型的变量。

- **变量定义**

  指定了一个数据类型，并包含了该类型的一个或多个变量的列表。

  变量定义的作用是，告诉编译器在何处创建变量的存储，以及如何创建变量的存储。（变量只能被定义一次）

- **变量声明**

  向编译器保证变量以给定的类型和名称存在。（变量可以被声明多次）

- **变量是左值**

  左值（lvalue）表达式是指「指向内存位置的表达式」，如变量。左值可以出现在赋值号的左边或右边。

  而右值（rvalue）指存储在内存中某些地址的数值，如数值型的字面值。右值是不能对其进行赋值的表达式，即右值只能可以出现在赋值号的右边。

````c++
#include <iostream>
using namespace std;

//变量声明
extern int a;
extern int b;
extern int c;
extern float f;

int main()
{
    //变量定义及初始化（正确地初始化变量）
    int a = 11;
    int b = 22;
	int c = a + b;

	cout << c << endl;
	float f = 42.0/5.0;
    
    cout << f << endl;
    
    return 0;
}
````

- **C++变量作用域**

  作用域是程序的一个区域。

  | C++变量作用域 | 描述                                         | 备注                                                         |
  | ------------- | -------------------------------------------- | ------------------------------------------------------------ |
  | 局部变量      | 在函数或一个代码块内部声明的变量             | 只能被函数内部或代码块内部的语句使用，需要自行正确的初始化局部变量 |
  | 形式参数      | 在函数参数的定义中声明的变量                 | 在进入函数时被创建，退出函数时被销毁                         |
  | 全局变量      | 在所有函数外部（通常在程序的头部）声明的变量 | 全局变量可被任何函数访问，值在程序的整个生命周期内有效。全局变量系统会自动初始化（int、float 和 double 等类型为 `0`，而char类型为`\0`, 指针类型为 `NULL`。） |

````c++
#include <iostream>
using namespace std;

// 全局变量声明
int globalVar;

int main()
{
    //局部变量声明
    int a = 11;
    int b = 22;
    int c = a + b;
    
    cout << c << endl;
    
    int globalVar = a + b + c;
    cout << globalVar << endl;
    
    return 0;
}
````

注：若局部变量和全局变量重名，则函数内的局部变量的值会覆盖全局变量的值。

#### 常量

- **定义常量**

  常量是固定值（字面量），使用`#define identifier value` 或 `const type variable = value;` 定义。

- **整数常量**

  前缀指定基数（无前缀默认为十进制，0x 或 0X 代表十六进制，0 表示八进制），后缀是无符号整数 U 和 长整数 L 的组合。

  整数常量示例：`42，0234，0x3a，23，23u，23l，23ul`。

- **浮点常量**

  小数形式：必须包含整数部分、小数部分，或同时包含两者。如 `3.14159`。

  指数形式：必须包含小数点、指数，或同时包含两者。使用 e 或 E 引入引入带符号的指数。如 `314159E-5L`。

- **布尔常量**

  `true / false` 都是标准的 C++ 关键字（不应把 true 的值看成 1，把 false 的值看成 0）。

- **字符常量**

  宽字符常量（例如 L'x'）必须存储在 **wchar_t** 类型的变量中。

  窄字符常量（例如 'x'）可以存储在 **char** 类型的简单变量中。

- **字符串常量**

  使用双引号`“”`包含字符串，一个字符串包含类似于字符常量的字符：普通的字符、转义字符和通用的字符。可以使用空格做分隔符对长字符串进行分行。

【示例】定义常量

````c++
#include <iostream>

using namespace std;

// 使用 #define 定义常量
#define LENGTH 4
#define WIDTH 3

int main()
{
    int area;
    // 使用 const 关键字定义常量
    const char NEWLINE = '\n';
    
    area = LENGTH * WIDTH;
    cout << area << NEWLINE;
   
    return 0;
}
````



### 存储类

存储类说明符放置于所修饰的类型之前，用于定义 C++ 程序中变量/函数的范围（可见性）和生命周期。

| 存储类              | 描述                                                         | 备注                                                         |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| auto                | 声明变量时根据初始化表达式自动推断该变量的类型；声明函数时函数返回值的占位符 | C++17 开始，auto 不再是C++存储类说明符                       |
| register            | 用于定义存储在寄存器中的局部变量                             | C++17 弃用                                                   |
| static              | 指示编译器在程序的声明周期内保持局部变量的值                 | 修饰局部变量可在函数调用之间保持局部变量的值；应用于全局变量可以使变量的作用域限制在声明它的文件内；用在类数据成员上时，会导致仅有一个该成员的副本被类的所有对象共享。 |
| extern              | 用于提供一个全局变量的引用，即用来在另一个文件中声明一个全局变量或函数 | 常用于当两个或多个文件共享相同的全局变量或函数时             |
| mutable             | 允许对象的成员替代常量，即 mutable 成员可以通过 const 成员函数修改 | 仅适用于类的对象                                             |
| thread_local(C++11) | 使用 thread_local 声明的变量仅可在其上创建的线程上创建       | 仅应用于数据声明和定义；可与 static 或 extern合并使用        |



### 运算符

| 运算符种类     | 描述                                                         | 备注                                                       |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| 算术运算符     | `+, -, *, /, %, ++, --`                                      |                                                            |
| 关系运算符     | `==, !=, >, <, >=, <=`                                       |                                                            |
| 逻辑运算符     | `&&, ||, !`                                                  |                                                            |
| 位运算符       | `&, |, ^(按位异或)， ~(二进制补码运算符)， <<（左移）, >>（右移）` | 作用域位，并逐位执行操作                                   |
| 赋值运算符     | `=, +=, -=, *=, /=, <<=, >>=, &=, ^=, |=`                    |                                                            |
| `sizeof`运算符 | `sizeof`运算符返回变量的大小                                 |                                                            |
| 条件运算符     | `Condition ？X : Y`，可替代 `if…else` 语句                   | Condition为真，则值为 X，否则值为Y                         |
| 成员运算符     | 成员运算符`.`和`->`                                          | 用于引用类、结构体和共用体的成员                           |
| 强制转换运算符 | Cast                                                         | 用于把一种数据类型强制转换为另一种数据类型，如 int(3.14)   |
| 指针运算符     | `*`指向一个变量，`&`返回变量的地址                           |                                                            |
| 逗号运算符     | 逗号运算符`,`会顺序执行一系列运算                            | 整个逗号表达式的值是以逗号分隔的列表中的最后一个表达式的值 |

| 优先级（从高到低） | 运算符                            |
| ------------------ | --------------------------------- |
| 后缀               | `() [] -> . ++ --`                |
| 一元               | `+ - ！ ~ ++ -- (type)* & sizeof` |
| 乘除               | `* / %`                           |
| 加减               | `+ -`                             |
| 移位               | `<< >>`                           |
| 关系               | `< <= > >=`                       |
| 相等               | `== !=`                           |
| 位与 AND           | `&`                               |
| 位异或 XOR         | `^`                               |
| 位或 OR            | `|`                               |
| 逻辑与 AND         | `&&`                              |
| 逻辑或 OR          | `||`                              |
| 条件               | `?:`                              |
| 赋值               | `= += -= *= /= <<= >>= &= ^= |=`  |
| 逗号               | `,`                               |

注：一元运算符、条件运算符和赋值运算符的结合性为「从右到左」，其余均为「从左到右」。



### 控制流

#### 循环

- `while循环`
- `for循环`：C++偏向使用 `for(;;)`结构来表示一个无限循环。使用 `Ctrl + C` 可以终止一个无限循环。
- `do…while循环`
- 嵌套循环



#### 判断

`if`语句、`if…else` 语句、嵌套 `if`语句、`switch` 语句、嵌套`switch` 语句



### 函数

#### 函数的定义、声明和调用

````c++
// 函数声明
return_type function_name( parameter list );

int main()
{
    // 函数调用
    int i = function_name( parameter list );
}

// 函数定义
return_type function_name( parameter list )
{
   body of the function
}
````

| 调用类型         | 向函数传递参数的方式           | 备注                             |
| ---------------- | ------------------------------ | -------------------------------- |
| 传值调用（默认） | 将参数的**实际值**赋给形式参数 | 修改函数内的形参对实参**无**影响 |
| 指针调用         | 将参数的**地址**赋给形式参数   | 修改函数内的形参对实参**有**影响 |
| 引用调用         | 将参数的**引用**赋给形式参数   | 修改函数内的形参对实参**有**影响 |

注：可以为参数设置默认值。

#### Lambda 函数或表达式（匿名函数）

- Lambda 表达式把函数看做**对象**：将 Lambda 表达式赋给变量、作为参数传递、求值。

````c++
//	Lambda Function:	[capture](parameters)->return_type{body}

[](int x, int y)-> int { int z = x + y; return z + x;}

[](int x, int y){return x < y;}

//	Without Return:		[capture](parameters){body}
[]{ ++global_x; }

````

- Lambda 表达式的闭包行为：在 Lambda 表达式内可以访问当前作用域的变量，注意 C++变量传递有传值和引用的区别。

  | 通过[]指定 | 变量传递方式                             | 备注                               |
  | ---------- | ---------------------------------------- | ---------------------------------- |
  | `[]`       | 未定义任何变量，使用未定义变量会发生错误 | 需要显示传入，才能使用 `this` 指针 |
  | `[x, &y]`  | x - 传值方式（默认），y  - 引用方式      |                                    |
  | `[&]`      | 任何被使用到的外部变量 - 引用方式        | 可以直接使用 `this` 指针           |
  | `[=]`      | 任何被使用到的外部变量 -传值方式         | 可以直接使用 `this` 指针           |
  | `[&, x]`   | x -传值方式，其余变量 - 引用方式         |                                    |
  | `[=, &z]`  | z - 引用方式，其余变量 - 传值方式        |                                    |

  注：`[]`需要显示传入，才能使用 `this` 指针，即`[this](){ this->someFunc(); };`。



### 数学运算

需要使用 C++内置的数学函数时，需要引用头文件`<cmath>`。

- `double cos(double);`

- `double sin(double);`

- `double tan(double);`

- `double pow(double, double);`： `pow(3.14, 4.2)`返回 3.14 的4.2次方。

- `double hypot(double, double);`：参数为直角三角形的两直角边，求斜边。

-  `double sqrt(double);`

- `double floor(double);`

- `double fabs(double);`

- `int abs(int);`

  

随机数

````c++
#include <iostream>
#include <ctime>
#include <cstdlib>

using namespace std;

int main()
{   
    // 设置种子 - 生成随机数前必须先调用 srand()函数
    srand( (unsigned)time( NULL ) );
    
    //	生成 5 个随机数
    for(int i = 0; i < 5; i++)
    {
        // 	生成实际的随机数
        int j = rand();
        cout << j << "	";
    }
    
    cout << endl;
    return 0;
}
````



### 数组

- 数组的基本用法

````c++
#include <iostream>
using namespace std;

#include <iomanip>
using std::setw;	

int main()
{
    //	声明并初始化数组
    double myArray[10] = {1.0, 2.0, 3.0, 4.0};
    //	通过『索引』给数组元素赋值
	myArray[2] = 3.1;
    
    //	使用 setw()函数格式化输出：setw(n)中 n 表示宽度，只对紧接着的输出有作用，可配合 setfill()使用。
    cout << setw(4) << "Element" << setw(13) << "Value" << endl;
        
    //	输出数组元素
    for(int i = 0; i < 10; i++)
    {
     cout << setw(7)<< i << setw(13) <<  myArray[i] << endl;
    }

    return 0;
}	
````

- **二维数组**

  一维数组的数组。其他维度类似理解。

- **指向数组的指针**

  使用「数组名」作为常量指针，或使用常量指针做数组名。

- **传递数组给函数**

  将函数的形式参数声明为一个「指针、已定义大小的数组、或者未定义大小的数组」后，可以将数组传给一个函数，数组类型会自动转换为指针类型，因此传的实际是地址。

- **从函数返回数组**

  声明一个返回指针的函数后，可以从函数返回一个数组。虽然 C++不允许返回一个完整的数组作为函数的参数，但是可以通过制定不带索引的数组名来返回一个指向数组的的指针。



### 字符串

| 字符串                    | 描述                                        | 举例                        | 头文件     |
| ------------------------- | ------------------------------------------- | --------------------------- | ---------- |
| C风格字符串               | 使用 null字符 `\0`终止的一维字符数组        | `char name[] = "Lily";`     | `<ctring>` |
| C++引入的 `string` 类类型 | 支持C风格字符串的所有操作，并新增了一些功能 | `string myString = “Jobs”;` | `<string>` |

- **C风格字符串**

C++中用于操作以 null 结尾的字符串的函数：

| 函数              | 作用                                                        |
| ----------------- | ----------------------------------------------------------- |
| `strcpy(s1,s2);`  | 将字符串`s2`复制到`s1`                                      |
| `strcat(s1,s2);`  | 将字符串`s2`连接到`s1`的末尾，作用同`+`                     |
| `strlen(s1);`     | 返回字符串`s1`的长度                                        |
| `strcmp(s1,s2);`  | 相同返回 0，`s1`比`s2`小返回负数，`s1`比`s2`大返回正数      |
| `strchr(s1, ch);` | 返回一个指针，指向字符串`s1`的中字符 `ch`第一次出现的位置   |
| `strshr(s1, s2);` | 返回一个指针，指向字符串`s1`的中字符串 `s2`第一次出现的位置 |

````c++
#include <iostream>
#include <cstring>

using namespace std;

int main()
{
    char str1[] = "Hello "; 
    char str2[] = "world";
    char str3[13];
    int len;
    
    // 将 str1 复制到 str3
    strcpy( str3, str1 );
    cout << "strcpy(str3,str1): " << str3 << endl;
    
    // 连接 str1 和 str2 :将字符串 str2 连接到 str1的末尾
    strcat( str1, str2  );
    cout << "strcat(str1,str2): " << str1 << endl;
    
    // 连接后 str1 的总长度
    
    len = strlen(str1);
    cout << "strlen(str1): " << len << endl;
    
    cout << strcmp(str2,str3) << endl;
   
    return 0;
}
````

- C++中的 String 类

  ````c++
  #include <iostream>
  #include <string>
  
  using namespace std;
  
  int main()
  {
      
      string str1 = "Hello "; 
      string str2 = "world";
      string str3;
      int len;
      
      // 将 str1 复制到 str3
      str3 = str1 ;
      cout << "str3: " << str3 << endl;
      
      // 连接 str1 和 str2 :将字符串 str2 连接到 str1的末尾
      str3 = str1 + str2;
      cout << "str1 + str2 : " << str3 << endl;
      
      // 连接后 str1 的总长度
      
      len = str3.size();
      cout << "str3.size(): " << len << endl;
     
      return 0;
  }
  ````

  

### 指针

| 重点           | 描述                                                         | 备注                         |
| -------------- | ------------------------------------------------------------ | ---------------------------- |
| 指针           | 一个变量，用来存储变量的内存地址                             | `double *myPointer = NULL;`  |
| 指针的值       | 一个代表内存地址的**十六进制数**（另一个变量的地址，即内存变量的直接地址） | `0x7ffee0fb9aa0`             |
| 空指针         | 赋为 `NULL` 值的指针，`NULL` 指针是一个定义在标准库中的值为 0 （`0x0`）的常量 | `int *pointer = NULL;`       |
| 算术运算       | 可以对指针进行`++，--， +， -`四种算术运算                   | 递增 / 递减 指针             |
| 指针和数组     | 一个数组名对应一个指针常量，代表数组首地址                   | 可以把数组首地址赋给指针     |
| 指针数组       | 用数组存储某种数据类型的指针，即数组元素是指针               | `int *ptr[i] = myArray[i] ;` |
| 指针链         | 指向指针的指针，即多级间接寻址（指针链）                     | `int **pptr;`                |
| 传递指针给函数 | 通过**引用**或**地址**传递参数，使传递的参数在主调函数中被改变 | 声明函数参数为指针类型即可。 |
| 从函数返回指针 | 函数返回指针到局部变量、静态变量和动态内存分配               | `int *myFunction(){...}`     |



1. **不同数据类型的指针之间的差别**：指针所指向的变量或常量的数据类型不同。

2. **内存地址 0** ：地址为 0 的内存位置是 操作系统保留的，在大多数操作系统中都不允许程序访问。内存地址 0 的作用是，表明该指针不指针一个可访问的位置。如果指针包含空值（零值），则假定它不指向任何东西。可以使用 if 语句检查一个空指针。

   ````c++
   if(ptr)		// 如果 ptr 非空，则完成
   if(!ptr)	// 如果 ptr 为空，则完成
   ````

3. **指针的算术运算**：对指针进行递增（++）运算，是在不影响内存位置中实际值的情况下，移动指针到下一个内存位置。即把指针的值减去其数据类型对应的字节数。对指针进行递减同理。
4. **指针的比较**：两个指针指向两个相关的变量（如同一个数组中的不同元素）时，可以使用关系运算符对这两个指针进行比较。
5. **指针和数组**：指针和数组并非完全互换。可以把指针运算符`*`用在数组名（比如myArray）上，访问的是数组的第一个元素。比如`*myArray = i;`和`*(myArray + 2) = 33;`	都是合法的，但`myArray++;`是非法的。另外，也可以把指针存储在数组中。比如，可以用一个指向字符的指针数组来存储一个字符串列表。
6. **从函数返回指针**：局部变量未定义为 static 变量时，C++不支持在函数外部返回局部变量的地址。

【例】指针的基本用法：定义一个指针变量，把变量地址赋给指针，访问指针变量中可用地址的值，通过指针访问

````c++
#include <iostream>
using namespace std;

int main()
{
    double someVar = 3.14159;
    double *somePointer = NULL;	// 声明指针变量，并使用 NULL 初始化
    cout << "Initial Value of somePointer: " << somePointer << endl;
    
    somePointer = &someVar 		// 使用&运算符获取变量的内存地址，并存储在指针变量中
    
    cout << "Value of someVar: " << someVar << endl;			// 3.14159
    
    cout << "Value of somePointer: " << somePointer << endl;	// 一个十六进制数
    
    cout << "Value of *somePointer: " << *somePointer  << endl;	// 3.14159
    
    return 0;
}
````

【例】递增一个指针：数组是一个常量指针，而变量指针可以递增，所以使用指针代替数组，以便访问数组中的元素。

````c++
#include <iostream>
using namespace std;

#include <iomanip>
using std::setw;	

int main()
{
    const int ARRAYSIZE = 3;
    int someArray[ARRAYSIZE] = {11,22,33};
    int *somePointer = NULL;
    
    //	指针数组
    int *pointerArray[ARRAYSIZE];
    
    //	将数组名赋给指针
    somePointer = someArray;	
    
    //	格式化输出
    cout << setw(4) << "Address of someArray" << setw(37) << "Value of someArray" << endl;
    
    for(int i = 0; i < ARRAYSIZE; i++) 
    {
        pointerArray[i] = &someArray[i];	// 将每个数组元素的地址赋给指针数组
        
        //	下面两行代码功能相同
        //	cout << setw(4) << "someArray[" << i << "] : " << somePointer;
        cout << setw(4) << "someArray[" << i << "] : " << pointerArray[i];
        
        //	下面两行代码功能相同
        //	cout << setw(16) << "someArray[" << i << "] = " << *somePointer;
        cout << setw(16) << "someArray[" << i << "] = " << *pointerArray[i];
        
        cout << endl;
 		
        // 递增一个指针（移动到下一个位置）
        somePointer++;	
    }
    
    return 0;
}
````



【例】指针与数组并不能完全互换。

````c++
#include <iostream>
 
using namespace std;
 
int main ()
{
	const int ARRAYSIZE = 5;
    int myArray[ARRAYSIZE] = {11,22,33};

    for (int i = 0; i < ARRAYSIZE; i++)
    {
    	
    }

    for (int i = 0; i < ARRAYSIZE; i++)
    {
    	cout << myArray[i] << endl;
    }
 
    return 0;
}
````

【例】指针数组：用一个指向字符的指针数组来存储一个字符串列表。

````c++
#include <iostream>

using namespace std;

int main()
{
    const int ARRAYSIZE = 5;
    const char *courses[ARRAYSIZE] =	{
        "Math",
        "English",
        "Physics",
        "Biology",
        "Chemistry"
    };
    
    for(int i = 0; i < ARRAYSIZE; i++)
    {
        cout << "Value of courses[ " << i << " ] = ";
        cout << courses[i] << endl;
    }
    return 0;
}
````

【例】指针链

````c++
#include <iostream>

using namespace std;

int main()
{
    int var = 42;
    int *ptr = NULL;
    int **pptr = NULL;	// 多级间接寻址
    
    ptr = &var;			// 让指针 ptr 指向变量 var
    pptr = &ptr;		// 让指针 pptr 指向指针 ptr
    
    cout << "Value of var: " << var << endl;	// 42
    cout << "Value of ptr: " << ptr << endl;	// 存储变量 var 的内存地址(十六进制数)
    cout << "Value of pptr: " << pptr << endl;	// 存储指针 ptr 的内存地址(十六进制数)
    
    return 0;
}
````

【例】传递指针给函数：使用指针交换两个数。

````c++
#include <iostream>

using namespace std;

// Statement of swap()
void swap(double *pointer1, double *pointer2);

int main()
{

    double x = 1.2;
	double y = 3.4;

	cout << "Before swap: "<< endl;
	cout << "x = " <<  x << endl;
    cout << "y = " <<  y << endl;

    //call swap(): pass the pointer as parameter to the function swap()
    swap(&x, &y);

    cout << "After swapped: "<< endl;
    cout << "x = " <<  x << endl;
    cout << "y = " <<  y << endl;

    
    return 0;
}

// Definition of swap()
void swap(double *pointer1, double *pointer2)
{/* swap two numbers */
	double tmp = 0;
	
	tmp = *pointer1;
	*pointer1 = *pointer2;
	*pointer2 = tmp;
}
````

【例】函数接收数组做参数

```C++
#include <iostream>

using namespace std;

double getMax(double *myArray, int size);

int main()
{

    const int SIZE = 5;
    double myArray[SIZE] = {1.1, 5.5, 2.2, 4.4,3.3};
	double max = getMax(myArray, SIZE);

    cout << "Max value: " << max << endl;
    
    return 0;
}

double getMax(double *myArray, int size)
{
	double maxValue = myArray[0];
    for(int i = 1; i < size; i++)
    {
       if ( maxValue < myArray[i] )
        {
            maxValue = myArray[i];
        } 
        
    }
    return maxValue;
}
```

【例】从函数返回指针

```C++

```



### 引用

````c++
#include <iostream>

using namespace std;

int main()
{
    // 声明简单的变量
    int i = 42;
    double d = 3.1415926;
    
    // 声明引用变量
	int&  r = i;	// 创建引用：r 是一个初始化为 i 的整型引用
	double& s = d;
    
    cout << "Value of i : " << i << endl;
    cout << "Value of i reference : " << r << endl;
    
    cout << "Value of d : " << d << endl;
    cout << "Value of d reference : " << s << endl;
    
    return 0;
}
````

引用变量是一个别名，常用于函数参数列表和函数返回值。变量名称是变量附属在内存位置中的标签，引用是变量附属在内存位置中的第二个标签。可以通过原始变量名称或引用来访问变量的内容。

引用与指针的区别：

- 不存在空引用（引用必须连接到一块合法的内存）
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

与 C++ 引用相关的重要概念：

- C++ 支持把引用作为参数传给函数（比传一般的参数更安全）
- 从 C++ 函数中返回引用

````c++
#include <iostream>

using namespace std;

// 函数声明
void swap(int& x, int& y);
int main()
{
    // 局部变量声明
    int a = 42;
    int b = 9;
    
    cout << "交换前，a 的值：" << a << endl;
    cout << "交换前，b 的值：" << b << endl;
    
    swap(a,b);
    
    cout << "交换后，a 的值：" << a << endl;
   	cout << "交换后，b 的值：" << b << endl;
    
    return 0;
}

// 函数定义
void swap(int& x, int& y)
{
    int temp;
    temp = x;
    x = y;
   	y = temp;
    
    return;
}
````

````c++
/*
 *当函数返回一个引用时，则返回一个指向返回值的隐式指针。这样，函数就可以放在赋值语句的左边。
*/
#include <iostream>

using namespace std;

double vals[] = {1.2, 2.3, 3.4, 4.5, 5.6 };

double& setValues(int i)
{
    return vals[i]; 	// 返回第 i 个元素的引用
}

// 主函数要调用上面定义函数
int main()
{
    cout << "改变前的值" << endl;
    for (int i = 0; i < 5; i++ )
    {
        cout << "vals[" << i << "] = ";
        cout << vals[i] << endl;
    }
    
    setValues(1) = 0.2;	// 改变第 2 个元素
    setValues(3) = 0.4;	// 改变第 4 个元素
    
    cout << "改变后的值" << endl;
    for ( int i = 0; i < 5; i++ )
    {
       cout << "vals[" << i << "] = ";
       cout << vals[i] << endl;
    }
    return 0;
}
````





### 日期和时间

C++ 继承了 C 语言用于日期和时间操作的结构和函数。有四个与时间相关的类型：**clock_t、time_t、size_t** 和 **tm**。

类型 clock_t、size_t 和 time_t 能够把系统时间和日期表示为某种整数。

结构类型 **tm** 把日期和时间以 C 结构的形式保存，tm 结构的定义如下：

````c++
struct tm {
  int tm_sec;   // 秒，正常范围从 0 到 59，但允许至 61
  int tm_min;   // 分，范围从 0 到 59
  int tm_hour;  // 小时，范围从 0 到 23
  int tm_mday;  // 一月中的第几天，范围从 1 到 31
  int tm_mon;   // 月，范围从 0 到 11
  int tm_year;  // 自 1900 年起的年数
  int tm_wday;  // 一周中的第几天，范围从 0 到 6，从星期日算起
  int tm_yday;  // 一年中的第几天，范围从 0 到 365，从 1 月 1 日算起
  int tm_isdst; // 夏令时
};
````

| 序号 | 函数                                              | 说明                                                         |
| ---- | ------------------------------------------------- | ------------------------------------------------------------ |
| 1    | `time_t time(time_t *time);`                      | 返回系统的当前日历时间，自 1970 年 1 月 1 日以来经过的秒数。如果系统没有时间，则返回 -1。 |
| 2    | `char *ctime(const time_t *time);`                | 返回一个表示当地时间的字符串指针，字符串形式 *day month year hours:minutes:seconds year\n\0*。 |
| 3    | `struct tm *localtime(const time_t *time);`       | 返回一个指向表示本地时间的 **tm** 结构的指针                 |
| 4    | `clock_t clock(void);`                            | 返回程序执行起（一般为程序的开头），处理器时钟所使用的时间。如果时间不可用，则返回 -1。 |
| 5    | `char * asctime ( const struct tm * time );`      | 返回一个指向字符串的指针，字符串包含了 time 所指向结构中存储的信息，返回形式为：day month date hours:minutes:seconds year\n\0。 |
| 6    | `struct tm *gmtime(const time_t *time);`          | 返回一个指向 time 的指针，time 为 tm 结构，用协调世界时（UTC，即格林尼治标准时间GMT）表示。 |
| 7    | `time_t mktime(struct tm *time);`                 | 回日历时间，相当于 time 所指向结构中存储的时间               |
| 8    | `double difftime ( time_t time2, time_t time1 );` | 返回 time1 和 time2 之间相差的秒数                           |
| 9    | `size_t strftime();`                              | 用于格式化日期和时间为指定的格式                             |



````c++
/*
 *
 *获取当前系统的日期和时间，包括本地时间和协调世界时（UTC）
 *
 */

#include <iostream>
#include <ctime>	// 使用日期和时间相关的函数和结构时，需要在 C++ 程序中引用 <ctime> 头文件
 
using namespace std;
 
int main( )
{
   // 基于当前系统的当前日期/时间
   time_t now = time(0);
   
   // 把 now 转换为字符串形式
   char* dt = ctime(&now);
 
   cout << "本地日期和时间：" << dt << endl;
 
   // 把 now 转换为 tm 结构
   tm *gmtm = gmtime(&now);
   dt = asctime(gmtm);
   cout << "UTC 日期和时间："<< dt << endl;
    
   cout << "1970 到目前经过天数:" << (now /(24*3600)) << endl;
    
   tm *ltm = localtime(&now);
 
   // 使用结构 tm 格式化时间:输出 tm 结构的各个组成部分
   cout << "年: "<< 1900 + ltm->tm_year << endl;
   cout << "月: "<< 1 + ltm->tm_mon<< endl;
   cout << "日: "<<  ltm->tm_mday << endl;
   cout << "时间: "<< ltm->tm_hour << ":";
   cout << ltm->tm_min << ":";
   cout << ltm->tm_sec << endl;
}
````



### 结构体

````c++
#include <iostream>
#include <cstring>
 
using namespace std;
void printInfo( struct Books book );
void printBook( struct Books *book );

// 声明一个结构体类型 Books 
typedef struct Books 
{
    char title[50];
    char author[50];
    char subject[100];
    char source[100];
    int bookID;
    
}Books;

int main()
{
   // 定义结构体类型 Books 的变量 BookAboutOOP
    Books BookAboutOOP;	
    
    // 成员访问运算符（.）
    strcpy(BookAboutOOP.title, "Programming Abstractions In C++");	
    strcpy(BookAboutOOP.author, "Eric S. Roberts");
    strcpy(BookAboutOOP.subject, "OOP");
    strcpy(BookAboutOOP.source, "Stanford University-CS106B");
    BookAboutOOP.bookID = 123456;

    //  结构体作为函数参数   
    printInfo(BookAboutOOP);
    
   // 通过传 BookAboutOOP 的地址来输出信息： &结构体名称（查找结构变量的地址）
   printBook( &BookAboutOOP );
    
    return 0;
}

void printInfo( struct Books book ){
    cout << "标题 : " << book.title <<endl;
   	cout << "作者 : " << book.author <<endl;
   	cout << "主题 : " << book.subject <<endl;
    cout << "来源: " << book.source <<endl;
   	cout << "ID : " << book.bookID <<endl;
}

// 该函数以结构体指针作为参数
void printBook( struct Books *book )
{
   //使用指向该结构的指针访问结构的成员时，必须使用 -> 运算符
   cout << "Title  : " << book->title <<endl;	
   cout << "Author : " << book->author <<endl;
   cout << "Subject : " << book->subject <<endl;
   cout << "Source: " << book->source <<endl;
   cout << "ID : " << book->bookID <<endl;
}
````

- 声明一个结构体类型，定义结构体类型的变量
- 访问结构体成员
- 结构体作为函数参数
- 定义指向结构体的指针
- typedef 关键字

##  3.C++中的面向对象

### 3.1 类和对象

 定义C++类：定义了类的对象包括了什么（数据成员），以及在这个对象上可以执行的操作。可以把类当做一个带有函数的结构。

````c++
class classname						//class 类名
{
    Access specifiers;				//访问修饰符：private/protected/public
    	Data members/variables;		//数据成员：变量
   		Member functions(){}		//函数成员：方法
};									//一个类以分号结束
````

定义 C++对象：根据类来创建对象，声明类的对象与声明基本类型的变量一样。可以使用直接成员访问运算符`.`来访问类的对象的公共（public）属性和方法。

````c++
class Color
{
  public:			//注意：这里是冒号
    double red;
    double green;
    double blue;
};//类定义

Color RoomColor;	//声明 RoomColor，类型为 Color
````

- 类成员函数：把定义和原型写在类定义内部的函数。
- 类访问修饰符：类成员可以被定义为private（默认）、protected 或 public 。
- 类的构造函数：创建一个新的对象时调用。
- 类的析构函数：在删除所创建的对象时调用。
- C++拷贝构造函数：使用同一类中之前创建的对象来初始化新创建的对象。
- C++友元函数：可以访问类的 private 和 protected 成员。
- C++内联函数：通过内联函数，编译器试图在调用函数的地方扩展函数体中的代码。
- this 指针：每个对象都有一个特殊的指针 **this**，它指向对象本身。
- C++中的静态成员：类的数据成员和函数成员都可以被声明为静态的。

举例：修改例子

````c++
#include <iostream>

using namespace std;
class Room
{
    public:
    	double red;
    	double green;
    	double blue;
    //类成员函数声明
    	double get(void);
    	void set(double r, double g, double b);
};

//类成员函数定义
double Room::get(void)
{
 	return length*width*height;   
}
void Box::set(double len, double wid, double hei)
{
    length = len;
    width = wid;
    height = hei;
}

int main()
{
    Box Box1;
    Box Box2;
    Box Box3;
    double volume = 0.0;
    
    //box 1 详述
    Box1.height = 5.0;
    Box1.length = 6.0; 
   	Box1.breadth = 7.0;
 
   	// box 2 详述
  	Box2.height = 10.0;
 	Box2.length = 12.0;
   	Box2.breadth = 13.0;
    
    //box 1 的体积
    volume = Box1.height * Box1.length * Box1.width;
    cout << "Box1的体积：" << volume <<endl;
    
    // box 2 的体积
   volume = Box2.height * Box2.length * Box2.width;
   cout << "Box2 的体积：" << volume <<endl;
    
    //box 3 详述
    Box3.set(16.0, 8.0, 12.0);
    volume = Box3.get();
    cout << "Box3 的体积：" << volume <<endl;
    
    return 0;
}

//Box1 的体积：210
//Box2 的体积：1560
//Box3 的体积：1536
````



### 3.2 继承

````c++
//基类
class Animal 
{
    //eat()函数
    //sleep()函数
};

//派生类
class Human: public Animal 
{
    //think()函数
};
````

#### 继承

继承代表了 **is a** 关系，允许我们依据另一个类来定义一个类，从而实现代码复用并提高执行效率。

#### 基类和派生类

已有的类称为基类（base-class），新建的类被称为派生类(derived-class)。形式`class derived-class: access-specifier base-class`。一个派生类继承了除基类的构造函数、拷贝构造函数、析构函数、重载运算符、友元函数之外的所有基类方法。

#### 访问修饰符（access-specifier）

private（默认）、protected 或 public。派生类可以访问基类中所有的非私有成员，外部的类只能访问公有成员。

#### 继承类型

继承类型通过访问修饰符指定，几乎不使用 protected 或 private 继承，通常使用 public 继承。当使用不同类型继承时应遵循以下规则：

- 公有继承（public）：当一个类派生自公有基类时，基类的公有成员也是派生类的公有成员，基类的保护成员也是派生类的保护成员，基类的私有成员不能直接被派生类访问，但是可以通过调用基类的公有和保护成员来访问。
- 保护继承（protected）： 当一个类派生自保护基类时，基类的公有和保护成员将成为派生类的保护成员。
- 私有继承（private）：当一个类派生自私有基类时，基类的公有和保护成员将成为派生类的私有成员。



#### 多继承

````C++
class <派生类名>:<继承方式1><基类名1>,<继承方式2><基类名2>,…
{
<派生类类体>
};
````



### 3.3 重载函数和重载运算符

#### 函数重载

````c++
#include <iostream>
using namespace std;

class printData
{
    public:
    	void print(int i) {
            cout << "整数为：" << i << endl;
        }
    	void print(double f) {
            cout << "浮点数为：" << f << endl;
        }
    	void print(char c[]) {
            cout << "字符串为：" << c << endl;
        }
};//同名函数 print() 被用于输出不同的数据类型

int main(void)
{
    printData pd;
    
    //输出整数
    pd.print(42);
    //输出浮点数
    pd.print(3.14159);
    //输出字符串
    char c[] = "Hello World";
    pd.print(c);
    
    return 0;
}
````

**重载声明**：指一个与之前已经在该作用域内声明过的函数或方法具有相同名称的声明，但是它们的参数列表和定义（实现）不相同。

**函数重载**：C++允许在同一个作用域中的某个函数指定多个定义。在同一个作用域内，可以声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同。

当调用一个**重载函数**或**重载运算符**时，编译器通过把所使用的参数类型与定义中的参数类型进行比较，决定选用最合适的定义。选择最合适的重载函数或重载运算符的过程，称为**重载决策**。

#### 运算符重载

````c++
#include <iostream>
using namespace std;

class Box
{
    private:
    	double length;
    	double width;
    	double height;
    public:
    	double getVolume(void){
            return length * width * height;
        }
    	void setLength(double len){
            length = len;
        }
    	void setWidth(double wid){
            width = wid;
        }
    void setHeight(double hei){
        height = hei;
    }
    
    //重载 + 运算符，用于把两个 Box 对象相加
    Box operator+(const Box& b)
    {
        Box box;
        //对象作为参数进行传递，对象的属性使用 this 运算符进行访问
        box.length = this->length + b.length;
        box.width = this->width + b.width;
        box.height = this->height + b.height;
        return box;
    }
};

int main()
{
    Box Box1;
    Box Box2;
    Box Box3;
    double volume;
    
    //Box1 详述
    Box1.setLength(6.0);
    Box1.setWidth(7.0);
    Box1.setHeight(5.0);
    
    volume = Box1.getVolume();
    cout << "Volume of Box1:" << volume << endl;
    
    //Box2 详述
    Box2.setLength(12.0);
    Box2.setWidth(13.0);
    Box2.setHeight(10.0);
    
    volume = Box2.getVolume();
    cout << "Volume of Box2:" << volume << endl;
    
    //把两个对象相加，得到 Box3
    Box3 = Box1 + Box2;
    volume = Box3.getVolume();
    cout << "Volumn of Box3:" << volume << endl;
    
    return 0;   
}
````

C++ 允许在同一作用域中的**运算符**指定多个定义，称为**运算符重载**。重载的运算符是带有特殊名称的函数，函数名是由关键字 operator 和其后要重载的运算符符号构成的。与其他函数一样，重载运算符有一个返回类型和一个参数列表。

| 可重载的运算符 | 具体                                                         |
| -------------- | ------------------------------------------------------------ |
| 双目算术运算符 | \+ (加)，-(减)，*(乘)，/(除)，% (取模)                       |
| 关系运算符     | ==(等于)，!= (不等于)，< (小于)，> (大于)，<=(小于等于)，>=(大于等于) |
| 逻辑运算符     | \|\|（逻辑或）、&&（逻辑与）、！（逻辑非）                   |
| 单目运算符     | \+ (正)，-(负)，*(指针)，&(取地址)                           |
| 自增自减运算符 | ++(自增)，--(自减)                                           |
| 位运算符       | (按位或)，& (按位与)，~(按位取反)，^(按位异或),，<< (左移)，>>(右移) |
| 赋值运算符     | =, +=, -=, *=, /= , % = , &=,<<=, >>=                        |
| 空间申请与释放 | new, delete, new[ ] , delete[]                               |
| 其他           | **()**(函数调用)，**->**(成员访问)，**,**(逗号)，**[]**(下标) |

| 不可重载的运算符 | 说明               |
| ---------------- | ------------------ |
| `.`              | 成员访问运算符     |
| `.*`,`->*`       | 成员指针访问运算符 |
| `::`             | 域运算符           |
| `sizeof`         | 长度运算符         |
| `?:`             | 条件运算符         |
| `#`              | 预处理符号         |



### 3.4 多态

````c++
#include <iostream>

using namespace std;

class Shape {
    protected:
    	int width, height;
    public:
    	Shape(int a=0, int b=0)
        {
            width = a;
            height = b;
        }
    	virtual int area()
        {
            cout << "Parent class area:" <<endl;
            return 0;
        }//在 Shape 类中，area() 的声明前放置关键字 virtual
};

class Rectangle: public Shape{
    public:
    	Rectangle(int a=0, int b=0): Shape(a,b) { }
    int area()
    {
        cout << "Rectangle class area:" <<endl;
        return (width * height);
    }//每个子类都有一个函数 area() 的独立实现
};

class Triangle: public Shape {
   public:
    	Triangle(int a=0, int b=0): Shape(a,b) { }
    	int area()
        {
            cout << "Triangle class area:" << endl;
            return (width * height)/2;
        }//每个子类都有一个函数 area() 的独立实现
};

//程序的主函数
int main()
{
	Shape *shape;
    Rectangle rec(10,7);
    Triangle tri(10,5);
    
    //存储矩形的地址
    shape = &rec;
    //调用矩形的求面积函数 area
    shape->area();
    
    //存储三角形的地址
    shape = &tri;
    //调用三角形的求面积函数 area
    shape->area();
    
    return 0;
}
````

#### 多态

当类之间存在层次结构，并且类之间是通过继承关联时，就会用到多态。C++ 多态意味着调用成员函数时，会根据调用函数的对象的类型来执行不同的函数。一个基类被派生为多个类，每个子类都有一个函数 area() 的独立实现。这就是**多态**的一般使用方式。有了多态，就可以有多个不同的类，都带有同一个名称但具有不同实现的函数，函数的参数甚至可以是相同的。编译器看的是指针的内容。

#### 虚函数

在基类中使用关键字 **virtual** 声明的函数称为**虚函数** 。在派生类中重新定义基类中定义的虚函数时，会告诉编译器不要静态链接到该函数。

在程序中任意点可以根据所调用的对象类型来选择调用的函数，这种操作被称为**动态链接**或**后期绑定**。

**纯虚函数**：当我们想要在基类中定义虚函数，以便在派生类中重新定义该函数更好地适用于对象，但在基类中又不能对虚函数给出有意义的实现时，就会用到纯虚函数。

````c++
class Shape {
   protected:
      int width, height;
   public:
      Shape( int a=0, int b=0)
      {
         width = a;
         height = b;
      }
      // 纯虚函数
      virtual int area() = 0;// = 0 是在告诉编译器，函数没有主体
};
````





### 3.5 数据抽象和数据封装

````c++
#include <iostream>

using namespace std;

class Adder{
    public:
    	//构造函数
    	Adder(int i = 0)
   		{
        	total = i;
    	}
    
    	//对外的接口
    	void addNum(int number)
    	{
        	total += number;
    	};
    
    	//对外的接口
    	int getTotal()
    	{
        	return total;
    	};
    
    private:
    	//对外隐藏的数据
    	int total;
};

int main()
{
    Adder a;
    
    a.addNum(10);
    a.addNum(20);
    a.addNum(30);
    
    cout << "Total " << a.getTotal() <<endl;
    
    return 0;
}
````

#### 数据抽象

数据抽象将代码分离为「外部接口和内部实现」，只向外界提供关键信息，并隐藏其后台的实现细节。数据抽象既可以保护类的内部（不会因无意的用户级错误损害对象状态），也可以通过修改类实现满足需求的变化。在设计组件时，必须保持接口独立于实现。这样，即使改变了底层实现，接口也会保持不变，使用该接口的任何程序都不会受到影响，只要将最新的实现重新编译即可。

C++ 使用**类**来支持自定义抽象数据类型（ADT），从而为**数据抽象**提供了可能。它们向外界提供了大量用于操作对象数据的公共方法。C++ 程序中，任何带有公有和私有成员的类都可以作为数据抽象的实例。

比如，我们只需要知道公共接口，使用类 iostream的 cout 对象就可以输出数据到标准输出，而cout 的底层实现可以自由修改。

````c++
#include <iostream>
using namespace std;
 
int main( )
{
   cout << "Hello C++" <<endl;
   return 0;
}
````



#### 数据封装

程序函数是程序中执行动作的部分，会影响程序的信息（数据）。

**数据封装**是「将数据和操作数据的函数绑定」的机制，数据封装引申出了**数据隐藏**的概念 。

C++ 通过「创建**类**」来支持封装和数据隐藏（public、protected、private）。类包含私有成员（private）、保护成员（protected）和公有成员（public）。默认情况下，在类中定义的所有项目都是私有的。

应该尽可能地对外隐藏每个类的实现细节。保证良好的**封装性**，类成员状态一般都会设置为私有（private），如果不是必需就不暴露。数据成员、虚函数等所有成员都适用。

把一个类定义为另一个类的友元类，会暴露实现细节，从而降低了封装性。



### 3.6 接口（抽象类）

C++ 接口仅描述了类的行为和功能，使用**抽象类**实现。设计**抽象类**（ABC）是为了给其他类提供一个可继承的合适基类。抽象基类为所有的外部应用程序提供一个适当的、通用的、标准化的接口，抽象类不能被用于实例化对象，它只能作为**接口**使用。

如果类中至少有一个函数被声明为纯虚函数，则这个类就是抽象类。纯虚函数是通过在声明中使用 "= 0" 来指定的。

派生类通过继承抽象基类，可用于实例化对象的类被称为**具体类**。

举例：

````C++
#include <iostream>
using namespace std;

//基类
class Shape
{
    public:
    //提供框架接口的纯虚函数：抽象类定义了一个接口 getArea()
    virtual int getArea() = 0;	
    void setWidth(int w)
    {
        width = w;
    }
    void setHeight(int h)
    {
        height = h;
    }
    
    protected:
    int width;
    int height; 
};

//派生类：通过不同的计算面积的算法实现相同的函数
class Rectangle: public Shape
{
    public:
    	int getArea()
        {
            return (height * width);
        }
};
class Triangle: public Shape
{
    public:
    	int getArea()
        {
            return (height * width)/2;
        }
};

int main()
{
    Rectangle Rect;
    Triangle Tri;
    
    Rect.setWidth(5);
    Rect.setHeight(7);
    
    //输出对象的面积
    cout << "Total Rectangle area: " << Rect.getArea() << endl;
    
    Tri.setWidth(5);
    Tri.setHeight(7);
    //输出对象的面积
    cout << "Total Triangle area: " << Tri.getArea() << endl;
    
    return 0;
}
````



## 4.C++高级主题

### 4.1 文件和流

````c++
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
    char data[100];
    
    //以写模式打开文件
    ofstream outfile;
    outfile.open("afile.dat");
    
    cout << "Writing to the file" << endl;
    cout << "Enter your name:";
    cin.getline(data,100);
    
    //向文件写入用户输入的数据（使用流插入运算符 << 向文件写入信息）
    outfile << data << endl;
    
    cout << "Enter your age: ";
    cin >> data;
    cin.ignore();
    
    //再次向文件写入用户输入的数据
    outfile << data << endl;
    
    //关闭打开的文件
    outfile.close();
    
    //以只读方式打开文件
    ifstream infile;
    infile.open("afile.dat");
    
    cout << "Reading from the file" << endl;
    infile >> data;
    
    //在屏幕上写入数据
    cout << data << endl;
    
    //再次从文件读取数据并显示（使用流提取运算符 >> 从文件读取信息）
    infile >> data;
    cout << data << endl;
    
    //关闭打开的文件
    infile.close();
    
    return 0;
}
````

#### 打开和关闭文件

从文件读取信息或者向文件写入信息前，必须先使用 open()函数打开文件，而在程序终止前应关闭所有打开的文件。open() 函数和close() 函数都是 fstream、ifstream 和 ofstream 对象的成员。

````c++
//open()函数：第一参数指定要打开的文件的名称和位置，第二个参数定义文件的打开模式
void open(const char *filename, ios::openmode mode);

//以写入模式打开文件，并截断文件(以防文件已存在)
ofstream outfile;
outfile.open("file.dat", ios::out | ios::trunc );

//打开一个文件用于读写
ifstream  afile;
afile.open("file.dat", ios::out | ios::in );

//close()函数
void close();
````

| 打开模式   | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| ios::app   | 所有写入都追加到文件末尾                                     |
| ios::ate   | 文件打开后定位到文件末尾                                     |
| ios::in    | 打开文件用于读取                                             |
| ios::out   | 打开文件用于写入                                             |
| ios::trunc | 若该文件已存在，其内容将在打开文件前被截断（把文件长度设为 0） |

注：可以通过符号`|`把以上两种或两种以上的模式结合使用。



#### 写入和读取文件

````c++
...
outfile << data << endl;	//使用流插入运算符 << 向文件写入信息
...
...
infile >> data;				//使用流提取运算符 >> 从文件读取信息
...
````



#### 文件位置指针

**istream** 和 **ostream** 都提供了用于重新定位文件位置指针的成员函数。这些成员函数包括关于 istream 的 **seekg**（"seek get"）和关于 ostream 的 **seekp**（"seek put"）。

seekg 和 seekp 的参数通常是一个长整型。第二个参数可以用于指定查找方向。查找方向可以是 **ios::beg**（默认的，从流的开头开始定位），也可以是 **ios::cur**（从流的当前位置开始定位），也可以是 **ios::end**（从流的末尾开始定位）。

文件位置指针是一个整数值，指定了从文件的起始位置到指针所在位置的字节数。

````c++
//定位到fileObject的第 n 个字节（假设是 ios::beg）
fileObject.seekg(n);

//把文件的读指针从 fileObject 当前位置向后移 n 个字节
fileObject.seekg(n,ios::cur);

//把文件的读指针从 fileObject 末尾往回移 n 个字节
fileObject.seekg(n,ios::end);

//定位到 fileObject 的末尾
fileObject.seekg(0,ios::end);
````



### 4.2 异常处理

#### C++标准异常

C++ 提供了一系列以父子类层次结构组织起来的标准的异常，定义在 `<exception>` 中。

![C++ 异常的层次结构](img/exceptions_in_cpp.png)

| C++标准异常            | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| **std::exception**     | 所有标准 C++ 异常的父类                                      |
| std::bad_alloc         | 可以通过 **new** 抛出                                        |
| std::bad_cast          | 可以通过 **dynamic_cast** 抛出                               |
| std::bad_exception     | 处理 C++ 程序中无法预期的异常                                |
| std::bad_typeid        | 可以通过 **typeid** 抛出                                     |
| **std::logic_error**   | 理论上可以通过读取代码来检测到的异常                         |
| std::domain_error      | 使用无效数学域时，抛出该异常                                 |
| std::invalid_argument  | 使用无效参数时，抛出该异常                                   |
| std::length_error      | 创建了太长的 std::string 时，抛出该异常                      |
| std::out_of_range      | 该异常可以通过方法抛出，如 `std::vector` 和 `std::bitset<>::operator[]()` |
| **std::runtime_error** | 理论上不可以通过读取代码来检测到的异常                       |
| std::overflow_error    | 发生数学上溢时，抛出该异常                                   |
| std::range_error       | 尝试存储超出范围的值时，抛出该异常                           |
| std::underflow_error   | 发生数学下溢时，抛出该异常                                   |

#### 通过继承和重载 **exception** 类定义新的异常

````c++
#include <iostream>
#include <exception>

using namespace std;

struct MyException : public exception
{
    const char * what () const throw ()
    {
        return "C++ Exception";
    }//what() 是异常类提供的一个公共方法，它已被所有子异常类重载。
};

int main()
{
    try
    {
    	throw MyException();    
    }catch(MyException& e)
    {
        std::cout << "MyException caught" << std::endl;
        std::cout << e.what() << std::endl;
    }catch(std::exception& e)
    {
        //其他错误
    }
}
````



````c++
/*使用 try/catch 语句的语法*/
try
{
    //保护代码（放置可能抛出异常的代码）
}catch( ExceptionName e1 )
{
    //catch 块
}catch( ExceptionName e2 )
{
    //catch 块
}catch( ExceptionName eN )
{
    //catch 块
}
````



异常提供了一种转移程序控制权的方式。C++ 异常处理涉及到三个关键字：**try、catch、throw**。如果 **try** 块在不同的情境下会抛出不同的异常，可以尝试罗列多个 **catch** 语句，用于捕获不同类型的异常。

| 关键字 | 用途                                                         |
| ------ | ------------------------------------------------------------ |
| throw  | 当问题出现时，程序会抛出一个异常                             |
| catch  | 捕获异常                                                     |
| try    | **try** 块中的代码标识将被激活的特定异常，其后通常跟着一个或多个 catch 块 |

使用 **throw** 语句在代码块中的任何地方抛出异常。throw 语句的操作数可以是任意的表达式，表达式的结果的类型决定了抛出的异常的类型。

````c++
//除以零时抛出异常
double division(int a, int b)
{
    if( b==0 )
    {
        throw "Division by zero condition!";
    }
    return (a/b);
}

int main()
{
    int x = 50;
    int y = 0;
    double z = 0;
    
    try{
        z = division(x,y);
        cout << z << endl;
    }catch(const char* msg) {
        cerr << msg << endl;
    }
    
    return 0;
}
````



### 4.3 动态内存

````c++
#include <iostream>
using namespace std;

int main()
{
	double* pValue = NULL;			//初始化为 null 的指针
    
	if(!(pValue = new double)){		// 使用 new 运算符动态分配内存
    	cout << "Error: out of memory." << endl;
    	exit(1);
	}
    
 	*pValue = 29494.99;     		// 在分配的地址存储值
  	 cout << "Value of pValue : " << *pValue << endl;
	delete pValue;			// 使用 delete 操作符释放 pvalue 所指向的内存
    
    return 0;
}

//Value of pvalue : 29495
````

#### 栈和堆

C++ 程序中的内存分为两个部分：栈（在函数内部声明的所有变量都将占用栈内存）和堆（程序中未使用的内存，在程序运行时可用于动态分配内存）。动态内存分配与堆存储管理有关。在 C++中，我们可以使用 new 操作符和 delete 操作符实现动态内存分配。

- **new 操作符**：为任意的数据类型动态分配内存（包括分配内存，创建对象）。C 语言的malloc() 函数在 C++ 中仍然存在，但不建议用。new 不只分配了内存，还创建了对象。
- **delete 操作符**：释放已经动态分配内存的变量所占用的内存。

#### 数组的动态内存分配

- 字符数组

````c++
char* pValue = NULL;		// 初始化为 null 的指针
pValue = new char[20];		// 为变量请求内存

delete [] pValue;			// 删除 pValue 所指向的数组
````

- 一维数组

````c++
//	动态分配（数组长度为 n)
int *array = new int [n];

// 释放内存
delete [] array;
````

- 二维数组

````c++
int **array
// 假定数组第一维长度为 m， 第二维长度为 n
// 动态分配空间
array = new int *[m];
for( int i=0; i<m; i++ )
{
    array[i] = new int [n]  ;
}
//释放
for( int i=0; i<m; i++ )
{
    delete [] array[i];
}
delete [] array;
````

- 三维数组

````c++
// 假定数组第一维为 m， 第二维为 n， 第三维为h
int ***array;	
// 动态分配空间
array = new int **[m];
for( int i=0; i<m; i++ )
{
    array[i] = new int *[n];
    for( int j=0; j<n; j++ )
    {
        array[i][j] = new int [h];
    }
}
//释放
for( int i=0; i<m; i++ )
{
    for( int j=0; j<n; j++ )
    {
        delete[] array[i][j];
    }
    delete[] array[i];
}
delete[] array;
````



#### 对象的动态内存分配

````c++
#include <iostream>
using namespace std;

class Box
{
  public:
    Box(){
        cout << "调用构造函数！" << endl;
    }
    ~Box(){
        cout << "调用析构函数！" << endl;
    }
};

int main()
{
    Box* myBoxArray = new Box[4];
    
    delete [] myBoxArray;	//删除数组
    
    return 0;
}
````





### 4.4 命名空间

````c++
//	定义命名空间
namespace namespace_name {
    //代码声明
}

//调用带有命名空间的函数或变量时，需要在前面加上命名空间的名称
name::code;	//	code 可以是变量或函数
````

举例：

````c++
#include <iostream>
using namespace std;

//第一个命名空间
namespace first_space {
    void func(){
        cout << "Inside first_space" << endl;
    }
}

//第二个命名空间
namespace second_space {
    void func(){
        cout << "Inside second_space" << endl;
    }
}

using namespace second_space;
int main()
{
    //调用第一个命名空间中的函数
    first_space::func();
    
    //调用第二个命名空间中的函数
    func();
    
    return 0;
}
````



**命名空间（namespace）**：作为附加信息来区分不同库中相同名称的函数、类、变量等。使用了命名空间即定义了上下文。本质上，命名空间就是定义了一个范围。

一个文件夹(目录)中可以包含多个文件夹，每个文件夹中不能有相同的文件名，但**不同文件夹中的文件可以重名**。

使用 **using namespace** 指令，在使用命名空间时就不用在前面加上命名空间的名称。这个指令会告诉编译器，后续的代码将使用指定的命名空间中的名称。**using** 指令引入的名称遵循正常的范围规则。名称从使用 **using** 指令开始是可见的，直到该范围结束。此时，在范围以外定义的同名实体是隐藏的。

using 指令也可以用来指定命名空间中的特定项目。比如`using std::cout;`表示只使用 std 命名空间中的 cout 部分。随后的代码中，在使用 cout 时就可以不用加上命名空间名称作为前缀，但是 **std** 命名空间中的其他项目仍然需要加上命名空间名称作为前缀。

````c++
#include <iostream>
using std::cout;
 
int main ()
{
 
   cout << "std::endl is used with std!" << std::endl;
   
   return 0;
}
````

#### 不连续的命名空间

命名空间可以定义在几个不同的部分中，因此命名空间是由几个单独定义的部分组成的。一个命名空间的各个组成部分可以分散在多个文件中。

所以，如果命名空间中的某个组成部分需要请求定义在另一个文件中的名称，则仍然需要声明该名称。下面的命名空间定义可以是定义一个新的命名空间，也可以是为已有的命名空间增加新的元素.

#### 嵌套的命名空间

````c++
namespace namespace_name1 {
   // 代码声明
   namespace namespace_name2 {
      // 代码声明
   }
}
//使用 :: 运算符来访问嵌套的命名空间中的成员
// 访问 namespace_name2 中的成员
using namespace namespace_name1::namespace_name2;
 
// 访问 namespace:name1 中的成员
using namespace namespace_name1;
````

````c++
#include <iostream>
using namespace std;
 
// 第一个命名空间
namespace first_space{
   void func(){
      cout << "Inside first_space" << endl;
   }
   // 第二个命名空间
   namespace second_space{
      void func(){
         cout << "Inside second_space" << endl;
      }
   }
}
using namespace first_space::second_space;
int main ()
{
 
   // 调用第二个命名空间中的函数
   func();
   
   return 0;
}
````



### 4.5 模板

#### 函数模板

模板是泛型编程的基础，泛型编程即以一种「独立于任何特定类型」的方式编写代码。

````c++
template <typename type> ret-type func-name ()
{
	//函数的主体    
}
````

举例：

````c++
#include <iostream>
#include <string>

using namespace std;

template <typename T> //T 是占位符
inline T const& Max (T const& a, T const& b)
{
    return a < b ? b : a;
}

int main()
{
    int i = 39;
    int j = 20;
    cout << "Max(i,j):" << Max(i,j) << endl;
    
    double f1 = 3.14159;
    double f2 = 2.718;
    cout << "Max(f1,f2):" << Max(f1,f2) << endl;
    
    string s1 = "Hello";
    string s2 = "World";
    cout << "Max(s1,s2):" << Max(s1,s2) << endl;
        
    return 0;
}
````

#### 类模板

````c++
template <class type> class class-name {
	//
}
````

定义了类 Stack<>，并实现了泛型方法来对元素进行入栈出栈操作。

````c++
#include <iostream>
#include <vector>
#include <cstdlib>
#include <string>
#include <stdexcept>

using namespace std;

template <class T>
class Stack {
    private:
    	vector<T> elems;	//元素
    public:
    	void push(T const&); //入栈
    	void pop();			 //出栈
   		T top() const;		 //返回栈顶元素
    	bool empty() const{
       		return elems.empty();
    	}
};

template <class T>
void Stack<T>::push (T const& elem)
{
    elems.push_back(elem);	//	追加传入元素的副本
}

template <class T>
void Stack<T>::pop()
{
    if (elems.empty()) {
        throw out_of_range("Stack<>::pop():empty stack");
    }
    elems.pop_back();		//删除最后一个元素
}

template <class T>
T Stack<T>::top() const
{
    if(elems.empty()){
        throw out_of_range("Stack<>::top(): empty stack"); 
    }
    return elems.back();
}

int main()
{
    try{
        Stack<int> intStack; //int 类型的栈
        Stack<string> stringStack;//string 类型的栈
        
        //操作 int 类型的栈
        intStack.push(7);
        cout << intStack.top() << endl;
        
        //操作 string 类型的栈
        stringStack.push("hello");
        cout << stringStack.top() << std::endl;
        stringStack.pop();
        stringStack.pop();
    }
    catch(exception const& ex){
        cerr << "Exception: " << ex.what() <<endl;
        return -1;
    }
    return 0;
}
````



### 4.6 预处理器



### 4.7 信号处理

信号是由操作系统传给进程的中断，会提早终止一个程序（Ctrl + C 产生中断）。针对定义在C++头文件`<csignal>`中的这些可以捕获的信号，可以采取适当的动作。

| 可以捕获的信号 | 说明                                     |
| -------------- | ---------------------------------------- |
| SIGABRT        | 程序的异常终止（如调用abort）            |
|                | 错误的算术运算（除以零或导致溢出的操作） |
| SIGILL         | 检测非法指令                             |
| SIGINT         | 程序终止（Interrupt）信号                |
| SIGSEGV        | 非法访问内存                             |
| SIGTERM        | 发送到程序的终止请求                     |



````c++
//	signal()函数捕获突发事件(参数1是信号的编号（整数），参数2是指向信号处理函数的指针)
oid (*signal (int sig, void (*func)(int)))(int); 
signal(registered signal, signal handler);			//容易理解的格式

//raise() 函数生成信号(带有一个整数信号编号作为参数)
int raise (signal sig);	
````

使用signal()函数：

````c++
#include <iostream>
#include <csignal>
#include <unistd.h>

using namespace std;


void signalHandler(int signum)
{
    cout << "Interrupt signal (" << signum << ") received.\n";
    //	清理并关闭
    //	终止程序
        
   exit(signum);
}
int main()
{
    //注册信号 SIGINT 和信号处理程序(必须使用 signal 函数来注册信号，并将其与信号处理程序相关联)
    signal(SIGINT, signalHandler);
    while(1){
        cout << "Going to sleep..." << endl;
        sleep(1);
    }
    
    return 0;
}
````

使用 raise()函数：

````c++
#include <iostream>
#include <csignal>
#include <unistd.h>
 
using namespace std;
 
void signalHandler( int signum )
{
    cout << "Interrupt signal (" << signum << ") received.\n";
 
    // 清理并关闭
    // 终止程序 
 
   exit(signum);  
 
}
 
int main ()
{
    int i = 0;
    // 注册信号 SIGINT 和信号处理程序
    signal(SIGINT, signalHandler);  
 
    while(++i){
       cout << "Going to sleep...." << endl;
       if( i == 3 ){
          raise( SIGINT);
       }
       sleep(1);
    }
 
    return 0;
}
````

### 4.8 多线程

多线程是多任务处理的一种特殊形式，多任务处理允许让电脑同时运行两个或两个以上的程序。一般情况下，两种类型的多任务处理：**基于进程和基于线程**。

- 基于进程：程序的并发执行。
- 基于线程：同一程序的片段的并发执行。

多线程程序包含可以同时运行的两个或多个部分。这样的程序中的每个部分称为一个线程，每个线程定义了一个单独的执行路径。

POSIX Threads 或 Pthreads 提供的 API 可在多种类 Unix POSIX 系统上可用，比如 FreeBSD、NetBSD、GNU/Linux、Mac OS X 和 Solaris。

````c++
#include <pthread.h>

//创建一个 POSIX 线程
pthread_create(thread,attr,strat_routine,arg)	
    
//终止一个 POSIX 线程
pthread_exit(status)			
    
//连接线程（阻碍调用程序，直到指定的 threadid 线程终止）
pthread_join(threadid,status)	
    
//分离线程
pthread_detach(threadid)		
````

例 1：



### 4.9 Web 编程







## 5. C++资源库

### 5.1 STL 教程

### 5.2 标准库



学习资料：



## 附录

### 1. C++新增的关键字（相比 C语言）

| 关键字       | 解释                                                         | 备注         |
| ------------ | ------------------------------------------------------------ | ------------ |
| class        | 声明一个类（C++ 面向对象设计的基础）                         | 封装         |
| this         | 返回调用者本身的指针                                         |              |
| template     | 模板                                                         | 泛型机制     |
| virtual      | 虚拟                                                         | 多态机制     |
| namespace    | 一种比类大的结构，用于在逻辑上组织类                         | 命名空间     |
| operator     | 操作符重载（C++特殊的函数）                                  |              |
| throw        | 通过 throw 关键字"抛出"一个异常                              | 异常处理     |
| try          | 在 try 中调用可能抛出异常的函数，然后在 try 后面的 catch 中捕获并进行处理 | 异常处理     |
| catch        | 和 try 语句一起用于异常处理                                  | 异常处理     |
| new          | 新建一个对象，new 运算符总是返回一个指针                     |              |
| delete       | 释放程序动态申请的内存空间。其后常是一个指针或者数组 []，且只能 delete 通过 new 关键字申请的指针，否则会发生段错误。 | 容器类型     |
| dynamic_cast | 允许在运行时刻进行类型转换                                   | 动态转换     |
| explicit     | "禁止单参数构造函数"被用于自动型别转换                       |              |
| asm          | (指令字符串)允许在 C++ 程序中嵌入汇编代码                    | 嵌入汇编代码 |
| private      | 私有的，只能在本类以及友元中访问                             | 访问控制     |
| protected    | 受保护的，只能在本类以及其继承类和友元中访问                 | 访问控制     |
| public       | 公有的，标明为 public 的字段可以在任何类访问                 | 访问控制     |
| friend       | 声明友元关系，友元可以访问与其有 friend 关系的类中的 private/protected 成员 | 友元         |
| inline       | inline（内联）函数的定义将在编译时在调用处展开，inline 函数一般由短小的语句组成 | 提高程序效率 |
| mutable      | 易变的                                                       |              |
| typeid       | 指出指针或引用指向的对象的实际派生类型                       |              |

注：[C++ 的关键字（保留字）完整介绍](https://www.runoob.com/w3cnote/cpp-keyword-intro.html)



### 2.C++的关键字（完整）

![image-20210216102240342](img/keyword_cpp.png)

### 2.常用的三字符序列

![image-20210216102342752](img/trigraphs_cpp.png)

### 3.转义字符

![image-20210216121251788](img/escChar.png)

### 4.头文件

| 头文件                  | 描述             | 备注 |
| ----------------------- | ---------------- | ---- |
| `<cmath>`               | 内置数学函数     |      |
| `<cstring>`及`<string>` | 字符串相关库函数 |      |

