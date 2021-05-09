## Swift 编码规范

#### Prefer `let`-bindings over `var`-bindings wherever possible

优先使用 `let` 而非 `var` 可以产生安全清晰的代码。



#### Prefer structs over classes

- 优先使用 `struct`，因为值类型更简单，容易分析。
- 除非你需要 `class` 才能提供的功能（ `identity` 或 `deinit`ializers）时，再使用 `class`。继承通常不是使用 `class` 的好理由，因为**多态**可以通过**协议**实现，而**重用**可以通过**组合**实现。



#### Make classes `final` by default

`class` 应该用 `final` 修饰，类中的定义（属性和方法等）也要尽可能使用 `final` 修饰。 组合通常比继承更合适，选择使用继承则很可能意味着在做出决定时需要更多的思考。



#### Omit type parameters where possible

当对接收者来说一样时，参数化类型的方法可以省略接收者的类型参数。省略多余的类型参数让意图更清晰。

```swift
struct Composite<T> {
	…
	func compose(other: Composite) -> Composite {
		return Composite(self, other)
	}
}
```



#### Return and break early

当你遇到某些操作需要通过条件判断去执行，应当尽早地退出判断条件。你可以用 `if` 声明或使用 `guard`（推荐）。使用 `guard`声明时编译器会强制要求你将 `return`, `break` 或者 `continue` 一起搭配使用，否则会产生编译时错误。

```swift
guard someArray.isEmpty else {
    return
}
// Use someArray here
```



#### Avoid Using Force-Unwrapping of Optionals

尽量不要通过强制解包（`foo!`）来获取关联值，这样很可能会导致运行时崩溃。

推荐使用 `if-let` ，`if let` 绑定可选类型产生了更安全的代码。也可以使用可选链。

```swift
if let foo = foo {
    // Use unwrapped `foo` value in here
} else {
    // If appropriate, handle the case where the optional is nil
}

// Call the function if `foo` is not nil. If `foo` is nil, ignore we ever tried to make the call
foo?.callSomethingIfFooIsNotNil()
```



#### Avoid Using Implicitly Unwrapped Optionals

foo 可能为 `nil` 时，尽可能使用用 `let foo: FooType?` 而不是 `let foo: FooType!`。明确的可选类型产生了更安全的代码。



#### Prefer implicit getters on read-only properties and subscripts

如果可以，省略只读属性和 `subscript` 的 `get` 关键字。

```swift
var myGreatProperty: Int {
	return 42
}

subscript(index: Int) -> T {
	return objects[index]
}
```



#### Always specify access control explicitly for top-level definitions

Top-Level 的函数、类型和变量，总是应该指定详尽的权限控制说明符。而在这些函数或类型的内部，可以在合适的地方使用隐式权限控制。



#### When specifying a type, always associate the colon with the identifier

当指定标示符的类型时，冒号要紧跟着标示符，然后空一格再写类型。

```swift
class SmallBatchSustainableFairtrade: Coffee { ... }

let timeToCoffee: NSTimeInterval = 2

func makeCoffee(type: CoffeeType) -> Coffee { ... }

let capitals: [Country: City] = [sweden: stockholm]
```



#### Only explicitly refer to `self` when required

当调用 `self` 的属性或方法时，默认隐式引用`self`，这样保持了简洁性。参数名冲突时等等必要时再加上 `self`。在（逃逸）闭包里使用 `self` 凸显了它捕获 `self` 的语义，参数名冲突时使用 `self`也是在必要时使用。



#### Whitespace

- 使用 Tab 留空白
- 文件结束时留一个空行
- 使用足够的空行分割代码，使 代码成为合理的块
- 不要在一行结尾留下空白，也别在空行留下缩进
- 为了提高代码可读性，当定义操作符时，两边留空格。因为操作符 由标点字符组成，当立即连着类型或者参数值，会让代码非常难读。

关于空行和缩进，推荐使用 XCFormat ( 可在 App Store 搜索下载)。