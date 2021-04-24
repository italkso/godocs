## SwiftUI

### 1. 概述

```swift
import SwiftUI

struct SwiftUIView: View {
    var body: some View {
        Text("Hello World")
            .font(.headline)
            .foregroundColor(.white)
            .padding()
            .background(Color.primary)
            .cornerRadius(8.0)
    }
}
```

#### 1.1 View 和 Modifier

**View** 和 **Modifier **是声明式 UI 框架 **SwiftUI** 的核心 。比如，代码`Text("Hello World") .font(.headline)`，表示`Text View`被字体修改器 `.font(.headline)` 修改。界面功能由 Swift 配合框架实现，比如播放歌曲、点击按钮后触发付款流程、复制到剪贴板等。 

- **View**

  可见的界面元素（按钮、文字、滑条、图片、列表、应用底部按钮等），界面元素的位置关系（ZStack、VStack、HStack等）。

- **Modifier**

  修改视图的显示及运作方式，比如字体大小和种类、圆角、动画触控反馈、阴影、边际、背景等界面细节。



#### 1.2 SwiftUI 应用程序的组成

- **Apps 应用**

  `struct ReaderAPP ：{...}`，负责告知「代码归属同一应用」。`@main` 标识的地方为「应用进入点」。

- **Scenes 场景**

   `var body: some Scene {...}`，负责处理「应用多开」。

- **Views 视图**

  `struct ContentView: view {...}`，应用程序中将「呈现的视图」。

  

#### 1.3 数据流动

将与特定 View 相关的数据封装进 View 的视图结构中，可以使用达到「复用」Views 的目的。

**Manage Mutable Values as State**

```swift
 @State private var isSearch: Bool = false
```

你可以使用属性包装器 `@State`声明一个变量，用来存储视图中可能被修改的数据。声明为 `@State` 的变量就是状态属性（state properties），仅用于管理那些会影响到 UI 的瞬时状态（transient state ），比如按钮的高亮状态、过滤设置或者当前选择的列表项。你不应该将状态属性用作数据的持久存储（persistent storage）。

**Share Access to State with Bindings**

<img src="images/SwiftUI-MUIS-Overview@2x.png" alt="A diagram showing state stored in one view, shared with another view through" style="zoom:50%;" />

为了保证在多个Views 中共享数据的一致性，要遵循**唯一真值原则（Single Source of Truth**），这是数据流动中的重要思想。用户无论处在应用程序的哪一个视图结构中，其信息只应该被存储一次。因此，在子视图中应该使用 `@Binding` 与父视图中，即那些声明为 `@State` 的变量进行绑定。这样，多个视图之间就可以共享对状态属性的控制。

```swift
@Binding var isSearch: Bool
```

注意，绑定（binding）只是对状态属性的引用，@Binding 变量本身并不拥有一份存储。

使用美元符号 `$`作为前缀可以传递变化，如`$isSearch`。

**Animate State Transitions**

视图（View）状态发生变化时，SwiftUI 会立即更新该状态变化影响到的视图。你可以添加平滑的视觉过渡，方法是调用`withAnimation(_:_:)` 并将修改状态的代码放入该函数的尾随闭包（trailing closure）中。如果你仅仅是想针对某个特定的页面有过渡效果，使用`animation(_:)` 视图修改器就好了。



### 2. UI 与交互层面

#### 常用视图

```swift
// 文本视图

@state var username = ""
@state var password = ""
@State var textInput = ""

var body: some View {
    Text("Hello, World!")
	Label("显示文字", systemImage: "SF Symbol 图标名称")
	TextField("占位文字", text: $username)
    SecureField("占位文字", text: $password)
}
```

#### 视图运作原理

在 SwiftUI 中，由每个视图自行索要大小。当视图中内容大小明确时，视图根据自身需求索要空间。当视图本身内容大小不明确时，该视图会索要全部剩余空间。

操作系统会告知应用其**视图可用总空间的大小 （Proposed Size）**，该大小会层层传递给子级视图，子级视图会根据自身需求，用两种方式**索要大小 （Claimed Size）。**

SwiftUI 会将被索要的大小从总空间中剔除，并将剩余空间继续传给其它子级视图。在视图大小的传递过程中，SwiftUI 的作用是尽量协调并尊重每个视图索要的区域。空间不够时，则 SwiftUI 会在自身可控范围内适当压缩间距大小。如果空间还不够，则会协调视图相互妥协。



#### 视图内布局

- 使用指定大小的框架修改器`.frame()`直接告知系统视图需要的大小。

- 使用`.fixedSize()`锁定尺寸。

- 使用`.padding()`边缘留白。

-  使用`.ignoresSafeArea(.keyboard)` 和`.edgesIgnoringSafeArea(.all)`忽略安全区，其中`.all`可以替成`.leading`， `.trailing`， `.top`，` .bottom` ，`.vertical` ，`.horizontal`。

- 使用 `.hidden()`隐藏现有视图但保留视图位置。

- 使用`.redacted()`将尚未加载完成的数据自动转化为占位符。

  

#### 自定义修改器

```swift
import SwiftUI

struct SignInView: View {
    @State var username = ""
    @State var password = ""
    
    var body: some View {
        VStack {
            TextField("Username", text: $username) .inputFieldStyle()          
            SecureField("Password", text: $password).inputFieldStyle()
        }
    }
}

//  Create custom modifier - Step1
struct InputFieldModifirer: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.body)
            .foregroundColor(.primary)
            .textFieldStyle(RoundedBorderTextFieldStyle())
            .font(.headline)
            .frame(width: UIScreen.main.bounds.width / 1.1)
            .padding()
            .shadow(color: .secondary, radius: 5, x: 1, y: 5)
    }
}

// Create custom modifier - Step2
extension View {
    func inputFieldStyle() -> some View {
        self.modifier(InputFieldModifirer())
    }
}
```



### 4. 状态和数据流动（State & Data Flow）

> SwiftUI provides tools, like state variables and bindings, for connecting your app’s data to the user interface. These tools help you maintain a single source of truth for every piece of data in your app.

<img src="../images/SwiftUI-SaDF-Overview@2x.png" alt="A diagram showing how SwiftUI responds to external events and user inputs by" style="zoom:67%;" />

Image from [Apple Developer](https://docs-assets.developer.apple.com/published/4fee13b0ffd4854249fa6d4740449865/6075/SwiftUI-SaDF-Overview@2x.png)

**数据流动**（Data Flow） 指应用程序中数据的传递方式。

- 通过将值类型包装为[`State`](https://developer.apple.com/documentation/swiftui/state) 属性来在单个视图内管理UI状态的变化。
- 使用[`Binding`](https://developer.apple.com/documentation/swiftui/binding)属性包装器共享对唯一真值（ a source of truth）的引用，例如状态或可观察对象。
- 使用[`ObservedObject`](https://developer.apple.com) 属性包装器连接遵循[`ObservableObject`](https://developer.apple.com/documentation/Combine/ObservableObject)协议的外部引用模型数据。
- 使用[`EnvironmentObject`](https://developer.apple.com/documentation/swiftui/environmentobject)属性包装器访问存储在环境中的可观察对象(observable object)。
- 使用[`StateObject`](https://developer.apple.com/documentation/swiftui/stateobject)直接在视图中实例化可观察对象。
- 通过将值存储在[`Environment`](https://developer.apple.com/documentation/swiftui/environment)中，在整个应用程序中分配值。
- 使用[`PreferenceKey`](https://developer.apple.com/documentation/swiftui/preferencekey)从子视图向上通过视图层次结构传递数据。
- 使用[`FetchRequest`](https://developer.apple.com/documentation/swiftui/fetchrequest)管理与Core Data一起存储的持久性数据。
- `ObservableObject` 协议
- `@State`
- `@Binding`
- `@Environment`
- `@Published`
- `@StateObject`
- `@ObservedObject`
-  `@EnvironmentObject` 

「接收用户输入的数据」、「改变数据状态来更新界面、「渲染新内容」等由 SwiftUI 负责，开发者只需要使用由符号 **@** 表示的**属性包装器**（Property Wrapper）说明想要执行的操作。

@State、@Binding 和@Environment 是与数据流动有关的几个常见属性包装器。它们主要负责不同视图间的信息传递，视图与数据之间的沟通。



- **@State 状态**

  @State 的作用是将对应的变量全权交给 SwiftUI 进行内存和状态管理。即负责数据变化的状态，适用于在**当前视图**结构中可能会被修改的，需要驱动界面变化的变量。

  ```swift
  import SwiftUI
  
  struct TestView: View {
      
      @State private var isVisible = false
      
      var body: some View {
          
          ZStack {
              
              Toggle("Visible", isOn: $isVisible)
                  .font(.system(size: 20, weight: .bold, design: .rounded))
                  .padding()
                  .clipShape(Rectangle())
                  .background(Color.orange)
              
              if isVisible {
                  Text("Hello, World").font(.headline)
              }
          }
      }
  }
  ```

  

- **@Binding 绑定** 

  > If a view needs to share control of state with a child view, declare a property in the child with the [`Binding`](https://developer.apple.com/documentation/swiftui/binding) property wrapper. A binding represents a reference to existing storage, preserving a single source of truth for the underlying data. — [Managing-User-Interface-State](https://developer.apple.com/documentation/SwiftUI/Managing-User-Interface-State)

  在子视图中使用属性包装器 @Binding，能够将父视图结构的信息传递给子视图中的信息。无论出现多少个绑定，只存在唯一的真值。当修改绑定时，实际修改的是原有值。使用`$变量名`可以将绑定传递下去。

  

  ```swift
  import SwiftUI
  
  struct MySuperView: View {
      
      @State var userInput = ""
      
      var body: some View {
          VStack {
              MySubView(userInput: $userInput)
              AnotherSubView(userInput: $userInput)
          }
      }
  }
  
  struct MySubView: View {
      //	Add a binding variable in subview
      @Binding var userInput: String
      
      var body: some View {
          TextField("Enter your name",text: $userInput)
              .textFieldStyle(RoundedBorderTextFieldStyle())
              .padding()
              .background(Color.red)
              
      }
  }
  
  struct AnotherSubView: View {
      @Binding var userInput: String
      
      var body: some View {
          TextField("Enter your name",text: $userInput)
              .textFieldStyle(RoundedBorderTextFieldStyle())
              .padding()
              .background(Color.blue)
      }
  }
  ```

  

- **@Environment 环境**  

  属性包装器 `@Environment` 负责监听系统信息，环境中包含许多种由系统提供的信息，每个不同类别的信息叫做**环境值**（[EnvironmentValues](https://developer.apple.com/documentation/swiftui/environmentvalues)），比如 [`pixelLength`](https://developer.apple.com/documentation/swiftui/environmentvalues/pixellength),  [`scenePhase`](https://developer.apple.com/documentation/swiftui/environmentvalues/scenephase) 或者  [`locale`](https://developer.apple.com/documentation/swiftui/environmentvalues/locale)。

  ```swift
  //	Environment
  @Environment(\.locale) var locale: Locale
  @Environment(\.colorScheme) var colorScheme: ColorScheme
  
  // colorScheme
  if colorScheme == .dark { // Checks the wrapped value.
      DarkContent()
  } else {
      LightContent()
  }
  
  //	 Set or override some values using the environment(_:_:) view modifier 
  MyView().environment(\.lineLimit, 2)
  ```

  

  ### 5. 应用中的数据状态监测

  <img src="../images/mvvmCS193P.png" alt="MVVM Design Patern" style="zoom:67%;" />

- **Combine** 

  响应式框架 `Combine` 是 `SwiftUI` 中数据流动背后的驱动器，其中视图与数据的关系，「**视图是数据状态改变的结果 Views are a Function of State**」。

- **ObservableObject & @Published**

  **可观察对象**（`ObservableObject` ）是一个协议，该协议要求所有遵守该协议的类必须包含**发布器** （`@Published`）这个属性包装器。使用`@Published` 的目的是「标注哪些数据被改变时需要被发送」。当数据发生改变时，发布器会会自动将最新数据推送至所有订阅的视图中。

- **@ObservedObject**

  ````swift
  //	订阅可观察对象
  @ObservedObject var data: Data
  
  //	直接在视图中初始化并交由 SwiftUI 管理存储
  @StateObject var data = Data()	
  
  //	在最高层级的视图中把数据装到沙包里(丢沙包式)
  .environmentObject(data)
  //	跨视图使用（任意子视图中的写法 —— 接沙包）
  @EnvironmentObject var data: Data
  ````

  `@ObservedObject` 是放置在视图文件中，用于「订阅可观察对象」的属性包装器。 `@StateObject` 和 `@EnvironmentObject ` 是`@ObservedObject` 的两个变种。

  ```swift
  import SwiftUI
  
  class Data: ObservableObject {
      @Published var title = "Pride and Prejudice"
      @Published var author = "Jane Austen"
      @Published var content = "A single man in possession of a good fortune must be in want of a wife..."
  }//Data.swift - Provide data source for Apps
  ```

  

  ```swift
  import SwiftUI
  
  struct MyView: View {
  //    @ObservedObject var data: Data
      @StateObject var data = Data()
      
      var body: some View {
          FirstSubView().environmentObject(data)
      }
  }
  
  struct FirstSubView: View {
      var body: some View {
          SecondSubView()
      }
  }
  
  struct SecondSubView: View {
      @EnvironmentObject var data: Data
      
      var body: some View {
          VStack(alignment: .leading, spacing: 20) {
              Text(data.title)
                  .font(.headline)
                  .foregroundColor(.red)
              Text(data.author)
                  .font(.subheadline)
                  .foregroundColor(.secondary)
              Text(data.content)
                  .font(.body)
                  .padding(.vertical)
          }.padding()
      }
  }//	Use data from Data.swift
  ```

  

### 6. 数据存储

数据存储 （Data Persistence）表示本地或者云端存储。

#### FileManager

使用 FileManager 访问设备的本地存储空间，并将数据以 JSON 文件的形式储存。

- **准备数据模型(Model和 ViewModel)**

  

- **存取本地 JSON 文件**

  

- **用 FileManager 准备文件位置**

  Apple 各设备中的每个应用会拥有自己独立的存储空间，即采用了「沙盒存储机制」。使用 [**File Manager**](https://developer.apple.com/documentation/foundation/filemanager)可以访问沙盒。File Manager 隶属于 Foundation 框架，是文件存取的中介。

  操作系统管理设备上文件的方式叫做**文件夹路径**，每个应用的沙盒拥有一个独特的默认文件的文件夹路径。

  如果想要让应用支持读写，那么应用就需要获取该默认沙盒路径。语法如下：

  ```swift
  FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
  ```

- **读写本地 JSON 文件**

- **将存储步骤集成在 SwiftUI 中**

- **在 SwiftUI 中读取 JSON 文件**

### 7. UIFeedbackGenerator

[反馈生成器](https://developer.apple.com/documentation/uikit/uifeedbackgenerator) `UIFeedbackGenerator` 包含三个变种，分别是 `UINotificationFeedbackGenerator`，`UIImpactFeedbackGenerator` 和 `UISelectionFeedbackGenerator` 用于生成基础的震动反馈。



***Reference***

[1] <https://developer.apple.com/documentation/swiftui/state-and-data-flow>

[2] <https://developer.apple.com/documentation/SwiftUI/Managing-User-Interface-State>

