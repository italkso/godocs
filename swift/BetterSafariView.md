

## Safari Service

你可以通过「**外链 Link**」在应用中使用网页链接，不过它会使用户离开当前应用，跳转至应用外的网页。

```swift
Link(destination: URL(string: "https://www.example.com")!) {
    HStack {
    Text("Open in Safari")
            Image(systemName: "safari")
    }
}
```

你也可以在应用内打开 URL。此时，你可以使用Apple 的官方**浏览器服务框架 Safari Service** 或第三方库 [**BetterSafariView**](https://github.com/stleamist/BetterSafariView)。注意， API / 包 / 库 / 框架等都是**Package**。

你可以使用 Safari Service 框架将 Safari 行为集成到iOS 或 macOS 应用程序中，或者扩展 Safari 的行为。具体如下：

- 提供一个与Safari 界面几乎相同的用户界面。用户可以在此视图中浏览网页，然后返回到你的应用。(iOS)
- 在用户的 Safari 阅读列表中添加项目。(iOS)
- 从你的应用中确定你的内容拦截器扩展是否已加载，如果已加载，告诉它刷新其内容。(iOS和macOS)
- 实现Safari应用扩展。从你的应用中确定是否加载了Safari应用扩展。(MacOS)
- 将现有的Chrome、Firefox或Edge扩展程序转换为Safari网络扩展程序，或创建一个新的Safari网络扩展程序，可在其他浏览器中使用。(MacOS)
- 允许用户在应用程序和Safari之间共享cookie和网站数据，通过`SFAuthenticationSession`实现单点登录（SSO）体验。

我们也可以使用第三方库实现应用内跳转外部网页的目标。比如，我们可以通过 SPM（Swift Package Manager）导入 BetterSafariView，详细步骤如下：

- **粘贴网址**

  将 第三方库[BetterSafariView](https://github.com/stleamist/BetterSafariView) 在 GitHub 的网址粘贴至 Xcode 通过「File - Swift Packages - Add Package Dependency」弹出的界面地址栏中。

- **下载**

  点击 Next ，Xcode 将自动下载该三方库。在弹出的选项中保持默认的「Version: Up to Next Major」。

- **完成**

  点击「Finish」完成。

- **导入**

  `import BetterSafariView`

```swift
import SwiftUI
import BetterSafariView

struct ReadingNote: View {
    @State private var presentingSafariView = false

    var body: some View {
        NavigationView {
            ScrollView {
                VStack {
                    Link(destination: URL(string: "https://www.bing.com")!) {
                        RoundButton(text: "Open in Safari", image: "safari")
                    }

                    Button(action: {
                        self.presentingSafariView = true
                    }) {
                        RoundButton(text: "Open Links in this App", image: "arrow.up.forward.app")
                    }
                    .safariView(isPresented: $presentingSafariView) { SafariView(
                    
                        url: URL(string: "https://www.bing.com")!, configuration: SafariView.Configuration(
                        entersReaderIfAvailable: true, barCollapsingEnabled: true
                        )
                    )
                    .preferredBarAccentColor(.clear)
                    .preferredControlAccentColor(.orange)
                    .dismissButtonStyle(.close)
                    }
                }
            }
            .navigationTitle("Note")
        }
    }
}

```



**Reference**

[1] <https://developer.apple.com/documentation/safariservices>

