## SwiftUI 

### 核心概念

**View** 视图和 **Modifier **修改器是描述性 UI 编程框架 **SwiftUI** 的核心 。

代码`Text("Hello World") .font(.headline)`表示被字体修改器 `.font(.headline)` 修改的 `Text View` 。

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

**View**

可见的界面元素，比如按钮、文字、滑条、图片、列表、应用底部按钮等。界面元素的位置关系（ZStack、VStack、HStack）也属于 View 的范畴。

**Modifier**

修改视图的显示及运作方式，比如字体大小和种类、圆角、动画触控反馈、阴影、边际、背景等界面细节。

**界面功能**

由 Swift 配合及框架实现，比如复制到剪贴板，播放歌曲、点击按钮后触发付款流程等。 



### 常用视图

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

### 视图运作原理

在 SwiftUI 中，由每个视图自行索要大小。当视图中内容大小明确时，视图根据自身需求索要空间。当视图本身内容大小不明确时，该视图会索要全部剩余空间。

操作系统会告知应用其**视图可用总空间的大小 （Proposed Size）**，该大小会层层传递给子级视图，子级视图会根据自身需求，用两种方式**索要大小 （Claimed Size）。**

SwiftUI 会将被索要的大小从总空间中剔除，并将剩余空间继续传给其它子级视图。在视图大小的传递过程中，SwiftUI 的作用是尽量协调并尊重每个视图索要的区域。空间不够时，则 SwiftUI 会在自身可控范围内适当压缩间距大小。如果空间还不够，则会协调视图相互妥协。



### 视图内布局

- 使用指定大小的框架修改器`.frame()`直接告知系统视图需要的大小。

- 使用`.fixedSize()`锁定尺寸。

- 使用`.padding()`边缘留白。

-  使用`.ignoresSafeArea(.keyboard)` 和`.edgesIgnoringSafeArea(.all)`忽略安全区，其中`.all`可以替成`.leading`， `.trailing`， `.top`，` .bottom` ，`.vertical` ，`.horizontal`。

- 使用 `.hidden()`隐藏现有视图但保留视图位置。

- 使用`.redacted()`将尚未加载完成的数据自动转化为占位符。

  

### 自定义修改器