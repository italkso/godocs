## SwiftUI

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

注：Swift 编程语言详解 xdocs 文档。