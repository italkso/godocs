## Localization

根据不同地区的语言习惯和使用习惯差异对应用进行针对性调整，就是**应用本地化 (Localization)**。SwiftUI 框架已经自动处理好了很多本地化的问题，翻译是开发者主要需要做的本地化工作，涉及到商店描述、UI 界面和应用名称的翻译。你可以自己翻译，借助机器翻译（如[DeepL](https://www.deepl.com/translator)）或者聘请第三方翻译。

本地化需要考虑到语言差异，比如为所有字符串预留足够的长度，另外，也要考虑到使用习惯的差异。



### 商店描述本地化

- 翻译应用名称和标题

  [App Store Connect](https://appstoreconnect.apple.com) 的「App Information」分区

- **翻译应用描述**

  点击网站[App Store Connect](https://appstoreconnect.apple.com) 右侧的「+」按钮，可以添加应用描述所支持的语言。

- **翻译预览截图**

  长按应用程序图标，选择「Edit Scheme」，在弹出的界面中，找到「App Language 应用语言」，将其修改为待截图的目标语言。

- **Primary 语言**

  在开发者未提供对应内容的本地化翻译时，素材、简介、截图等信息的默认显示语言。

  

### UI 本地化流程

以中英文为例。

在 Xcode 中，依次选中「项目名 - Project 标签页」，选择 Localization 的选项，默认为「English - Development Language」 ，可以把英文当作代码层面的默认设置。点击「+」即可添加新的语言支持。

新建一个名为 `Localizable.strings`的「Strings File」，代表 UI 翻译文件 。

点击右侧的「Localize 」按钮后，在弹出的本地化选项中勾选英文和中文两种语言。勾选完成后，Xcode 会自动创建英文版和中文版的本地化文件，提供对应语言版本的值即可。



### 应用名称本地化

新建一个名为`InfoPlist.strings`的 Strings File，点击 「Localize」 按钮将 InfoPlist 文件分别创建两种语言的版本，打开对应的语言文件并进行翻译即可。之后在设备模拟器中切换系统语言，本地化应用名称即可正常显示。

