## 创建跨 Apple 生态系统的应用

SwiftUI 处理跨平台的思路是，**代码统一，但是保证各平台体验的独立性**。比如 Toggle 控件，在 iOS 、 iPadOS和 watchOS 中显示为椭圆形的「开关」，而在 macOS 中显示为「勾选框」，在 APPLE TV  中显示的是 「点入式菜单」。

我们可以使用 SwiftUI  在同一 Xcode 项目中添加支持 Mac、Apple TV、Apple Watch、iPhone、iPad 等平台的代码。不过，在调用某个框架时，你应当注意查看 APPLE 开发者文档，了解该框架中内容的可用性，从而判断 UI 在不同平台上的可用性。

- **创建跨平台应用**

  选择「Multiplatform - App」模版。创建一个跨 iPad、iOS、macOS 的应用，默认的UI 界面语言是 SwiftUI ，并且使用 SwiftUI Lifecycle 作为生命周期控制。

- **区分 iPhone 及 Mac 平台**

  如果 iPhone 及 Mac 平台仅有细微差异，就使用语法 `#if os(xxx) #endif` 进行针对性判断。

- **区分 iPadOS 及 iOS 平台**

   `UIDevice.current.userInterfaceIdiom == .pad` 为真表示运行在 iPad 上，反之运行在 iPhone 上。

- **给应用增加 Apple Watch 支持**

  在Xcode 顶部菜单栏中，选择「File - New Target」，然后在「watchOS - Application」下按需进行选择：

  - Watch App for iOS App - 依赖于 iOS 应用主体发布，无法单独在 Watch 应用商店中下载。

  - Watch App - 可以单独发布，不依赖任何 iOS 应用，可直接在 Watch 应用商店中下载的应用。

- **创建 Apple TV 应用**

  在Xcode 顶部菜单栏中，选择「File - New Target」，然后选择「tvOS - Application - App」创建 Apple TV 应用。

  

## Mac 应用运行方式

- **Mac (Designed for iPad)** 

  纯 iOS 应用，仅支持 M 芯片版 Mac。

- **Mac (Intel)** 

  纯 macOS 应用，仅支持 Intel 芯片版 Mac。

- **Mac (ARM)** 

  纯 macOS 应用，仅支持 M 芯片版 Mac

- **Mac (Rosetta)** 

  纯 macOS 应用，支持 M 及 Intel 芯片版 Mac。

- **Mac (Catalyst)** 

  纯 Mac 版 UIKit 应用，支持 M 及 Intel 芯片版 Mac。

- **Mac (Appkit)** 

  纯 Appkit 应用，支持 M 及 Intel 芯片版 Mac。



## 代码

```swift
import SwiftUI

struct ContentView: View {
    @State private var helloText = ""
    @State private var toggleOn = false

    var body: some View {
        VStack {
            Spacer()
            Toggle("Show Marked Only", isOn: $toggleOn)
                .padding()
                .font(.headline)
            Spacer()
            Text(helloText)
                .font(.title)
                .padding()
                .onAppear {
                    #if os(iOS)
                        helloText = "Hello, iOS"
                    #else
                        helloText = "Hello, macOS"
                    #endif
                    if UIDevice.current.userInterfaceIdiom == .pad {
                        helloText = "Hello, iPadOS"
                    }
                }
            Spacer()
        }
    }
}struct ContentView： View {
    @State var text = ""
    
    var body: some View {
        VStack {
            Text(text)
            	.onAppear {
                    #if os(iOS)
                    text = "iOS"
                    #else
                    text = "macOS"
                    #eddif
                    
                	if UIDevice.current.userInterfaceIdiom == .pad {
                        text = "iPadOS"
                    }
            	}
        }
    }
}
```
