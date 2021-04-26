## Xcode

### 1. 创建新项目

#### 使用模版创建 Xcode 应用

打开 Xcode，选择「Create a new Xcode project」，选择模板并对项目进行相关设置。

- **模板**

  Multiplatform App

- **项目设置**

  - Product Name
  - Team - Apple ID 
  - Organization Identifier （个人网站地址的倒置，邮箱名或其它唯一辨识信息）
  - Bundle Identifier （创作者识别码与项目名称的组合，自动生成）
  - Use Core Data 和 Host in CloudKit 暂不勾选
  - Include Tests （预置测试文件，勾选）

- **项目存储地点和选择**

  - 不建议使用iCloud，推荐将项目存在本机根目录中 Mac 自动创建的开发者 Developer 文件夹
  - 使用 Git 版本管理（勾选 Create Git repository on my Mac）

- **创建完成**

  点击Create完成项目创建。

### 2 . Xcode 界面

上下分别为运行 / 调试面板，左右分别为导航器 / 监视器面板，中部为主编辑面板。

#### 概念

- **负责 iOS 应用运行的 4 个文件**

  - **DemoApp.swift**

    应用程序入口

  - **ContentView.swift**

    文件包含程序的 UI 信息

  - **Assets.xcassets**

    所有媒体素材的存放地，如应用程序图标、颜色、图片、设计软件中导出的素材。

  - **Info.plist**

    Property List 属性列表类型文件，负责存储一些信息，并负责与目标设备沟通应用程序的基本信息。

    比如程序显示名是、是否支持横屏、为什么要申请使用相机等。

- **使用import 导入框架**

  使用 `import SwiftUI`导入 SwiftUI，就可以使用 Swift 及 SwiftUI 的内容了。不同框架为程序提供了不同的预设功能。

- **@main是应用程序的起点**

  **@main**位于导入框架后与代码开始之前。

- **项目运行顺序：App > Scene > View**

- **分类系统 Project - Target（项目与目标的关系）**

  Xcode 使用Project - Targets（项目 - 目标）分类系统 ，从而允许开发者将不同需求的资源从主项目中划分给不同目标。针对一个项目 Project（如 Demo），可以设定多个不同目标 Target（如 iOS 和 macOS）。

- **偏好设置**

  帐号登录：登录 Apple ID， 登录Git 远程版本管理工具（ 如GitHub）。



### 3. 工作流

#### 项目管理

- General （Identity，Deployment Info）
- Signing & Capabilities 
  - Signing：勾选「Automatically manage signing」自动管理签名，
  - Capabilities：Font，HealthKit， iCloud， In-App Purchase，Apple Pay。

#### 代码错误自动修复

- 报错提醒

  - 黄色警告，红色错误，紫色提醒。
  - Buildtime 问题：静态语法检查器错误和编译时发现的错误。
  - Runtime 问题：程序在运行时或用户操作触发的错误。

- 一键修复

  Fix（点击自动修复的前提是你理解为什么会出现这个错误）

#### 设备显示原理及素材导入

- **显示原理**

  Apple 通过「为更高物理分辨率的屏幕使用放大系数」来处理 Pixel 像素点，使物理分辨率（Pixel）和设计分辨率（Point ）脱钩。屏幕规格越高，物理分辨率密度越高的设备中，1 Point 所容纳的真实像素点数量更多。作为开发者，需要提供素材对应的 @1x、@2x、@3x 规格，保证应用程序在所有设备的屏幕上全部都能以最佳细节显示出来。

  - @1x：1 Point 对应 1 Pixel
  - @2x：1 Point 对应 2 Pixels ，如 iPhone 11是@2x设备 。
  - @3x：1 Point 对应 3 Pixels，如 iPhone 11 Pro是@3x设备。

- **颜色**

  - AccentColor（主题色 ，Any Appearance）- Universal

    选中 AccentColor 后，在右侧的监视器面板中切换选项卡至「Attributes Inspector」中。在 Appearance 一栏中选择「Any, Dark」选项来开启一个深色模式下此颜色的新色块。

  - 自定义颜色

    在主面板 AccentColor 下方的空白区域右键选择「Color Set」可自定义颜色。

- **图片**

  使用导入的某张图片作为按钮的背景时，需要选择图片后调出右侧的「Attributes Inspetctor」面板，在「Render as」一栏中选择「Original Image」。

- **设计素材**

  使用第三方软件制作后导出成@1x、@2x、@3x。

#### 开发者文档

按住 Option 按钮并点击屏幕上的任意关键词，快速查看文档，依次点击 Help - Developer Document 可以查看完整文档。

#### 调试

- **虚拟机调试**

  虚拟机调试是在 Mac 上直接运行程序的一种方式。每个版本的 Xcode 发布，都会自带与其系统版本匹配、机型不同的虚拟机。

  虚拟机在运行时使用的设备本质还是 Mac，虚拟机无法模拟所显示设备的真实硬件情况。在真实硬件中，iPhone 设备的内存一般在 2-4GB 左右，iPad 设备的内存一般在 3-6GB 左右。这些硬件区别极为重要，但虚拟机运行时不会有任何提醒，你在使用虚拟机测试时务必将真实情况纳入考量。

  当应用程序在虚拟机或真机运行时，你可以将 Xcode 左侧导航器面板切换到 Debug 选项卡中。在这个面板下，你可以看到应用程序当前使用的内存、CPU 占用量等信息。

- **真机调试**

  有线调试：使用数据线将真机接在 Mac 上。

  无线设备调试无线：同一个 Wi-Fi ，设置 Window - Devices and Simulators - Connect via network。



#### 应用图标制作

- 将 Sketch 模版定义为模版类型，避免误修改 Sketch 模版文件

  右键点击文件 Sketch 模版文件，点击「查看信息」，勾选「将此文件用作模版」即可。

- 将 SVG 图标导入 Sketch

- 取消圆角矩形蒙版

- 将图标导出到 Xcode 项目的AppIcon.appiconset中

- 更新 JSON 文件已保证图标自动链接

- 打开 Xcode 检查图标是否正确导出

- 测试图标

  

### 4. 效率提升

- **代码快速完成**

  输入代码时的智能预测

- **标签分页**

  双击不同文件，选中的文件以选项卡的形式出现在编辑器上方。

- **函数重命名**

  双击选中想要更改的名称，单击右键选择「Refactor - Rename」。

- **折叠条带**

  点击屏幕左侧的灰色条带，手动折叠条带标示区间的代码。

  偏好设置中勾选「Text Editing - Display」中的「Code folding ribbon」显示折叠条带。

- **断点调试**

  可以在代码中设置多个不同中断点（Breakpoint ），并在它们中间来回跳转，以便找到离程序问题最近的位置。在 Xcode 中，你可以点击左侧代码行数来添加中断点，不再需要此中断点时，将它的图标从行数上拖出窗口即可删除。

- **快速导航条**

  - 点击条中的任意文件夹来快速切换当前主编辑器中显示的文件。

  - 在已打开的代码文件中添加备注提醒等特殊标示，在开发者点击时快速跳转到文件中该备注的位置。标识符的具体使用格式为`// 标识符: - 文本`。常用的标识符：
    - MARK 划分小节
    - TODO 添加待办
    - FIXME 添加待修复

- **Library**

  点击右上角的「+」按钮，或者使用 `Command + Shift + L`调出Library，通过拖拽添加所需素材。

  - Views：SwiftUI 界面搭建

  - Modifiers：SwiftUI 界面搭建

  - Snippets：Swift 中常用的各种语法结构

  - Media：包含图片等文件

  - Color：包含 Assets 文件夹中自定义的所有颜色

- **Canvas**

  使用快捷键 `⌥ ⌘ Enter`开启画布（Canvas）显示， 快速、直观的预览代码（静态与实时预览）。画布专为 SwiftUI 服务，其顶部有 4 个按钮，分别是预览、在设备上运行、属性、增加预览。

  点击`Resume`可更新预览静态视图，点击`Live Preview`开启具有互动效果的实时预览。

  `ContentView_Previews: PreviewProvider` 要求 Xcode 在画布界面显示 ContentView 的预览，画布由此生成右侧代码预览。

  ```swift
  struct ContentView_Previews: PreviewProvider {
      static var previews: some View {
          ContentView()
      }
  }
  ```



### 5. 版本管理

- **Source Control**（顶部，版本管理菜单）

  - Cherry-Pick

    从已提交的、可能是其它分支的提交历史中，挑选出部分内容，并将其提交至当前分支中。

  - Stash

    **暂存**已修改、但未提交的内容

  - Discard

    **遗弃**已修改、但未提交的内容（一次性删除）

- **Source Control Navigator**（左侧，版本管理导航器）

  Branches、Tags、Remotes、Stashed Changes

- **Code Review**（右上，版本对比按钮）

- **Xcode 使用蓝色竖条和 M 字母提醒未 Commit 的内容**



### 6. 访问沙盒本地文件

- 选择菜单栏 「Window - Devices and Simulators」，选择应用运行的设备和查看沙盒的应用后，点击下方齿轮按钮，选择「Download Container」并存储。

- 存储好的沙盒信息为 `XXX.appdata`，右击该文件并选择「Show Package Content」。在打开的文件中，选择「AppData - Documents」即可查看沙盒内容。

