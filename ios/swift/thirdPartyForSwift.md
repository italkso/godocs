#  iOS 开发第三方开源库（Swift版）



## 1. 网络请求和交互

**[Alamofire](https://github.com/Alamofire/Alamofire)** 是一个「网络请求库」，**AF 命名空间**和**链式调用**是其主要特点。Alamofire 是 AFNetworking 的 Swift 语言版本，封装了 URL Loading System ，由 AFNetworking 作者 Mattt Thompson 负责开发维护。如果你使用 Objective-C 开发， 对应的网络请求库就是 AFNetworking。**[AlamofireImage](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dhttps%3A%2F%2Fgithub.com%2FAlamofire%2FAlamofireImage)** 是基于 Alamofire 的网络图片组件库。**[Moya](https://github.com/Moya/Moya)** 是一个基于 Alamofire 的更高层网络请求封装抽象层，作用同样是进行网络请求。

**[SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)** 是一个 「JSON 解析库」，SwiftyJSON 能够让开发者很方便的处理 Swift 中的数据，甚至处理嵌套复杂的 JSON 数据也不在话下。补充：ObjectMapper 也是一个 JSON 解析库。



## 2. 自动布局

**[SnapKit](https://github.com/SnapKit/SnapKit)** 是「 Autolayout 自动布局」，链式编程。如果你使用 Objective-C 开发， 可以使用自动布局框架 Masonry 。



## 3. 图片

**[Kingfisher](https://github.com/onevcat/Kingfisher)** 是由 onevcat 开源维护的「图片加载和缓存库」，采用了与 SDWebImage 相同的存储机制， 解决了从网络上下载图片和缓存图片的问题。如果你使用 Objective-C 开发， 可以使用 SDWebImage 实现网络图片的下载和缓存。

**[BSImagePicker](https://github.com/mikaoj/BSImagePicker)** 的用途时 「图片选取」，支持 Objective-C 和 Swift。

**[R.swift](https://github.com/mac-cain13/R.swift)** 的作用是「资源管理」，包括图片资源的管理，适合用在纯 Swift 项目中。



## 4. 数据库

**[Realm](https://realm.io/cn)** 是使用 C++ 开发的「跨平台移动数据库」，可用于 iOS 和 Android 的。支持 Java，Objective-C，Swift，React Native，Xamarin等平台。

**[FMDB](https://github.com/ccgus/fmdb)** 使用 Cocoa / Objective-C 封装了 「SQLite」。



## 5. 社交分享

**[MonkeyKing](https://github.com/nixzhu/MonkeyKing)** 是一个「社交分享」框架，它能够帮助开发者快速集成国内主流社交应用(微信、微博、QQ、支付宝)的分享、授权、支付等功能。



## 6. 图表

**[Charts](https://github.com/danielgindi/Charts)** 是一个很棒的「图表」框架，支持 iOS / tvOS / OSX 。



## 7. 动画

GitHub 上有人专门收集了一些主流的动画框架，包括 Objective-C 和 Swift，详情参见 **[awesome-ios-animation](https://github.com/ameizi/awesome-ios-animation)**。



## 8. 响应式编程

**[RxSwift](https://github.com/ReactiveX/RxSwift)** 是「函数响应式编程 (Funtional Reactive Programming) 」系列 ReactiveX 的 Swift 版本开源框架，核心就是「面向数据流编程」。

而 Objective-C 时代最流行的响应式框架 [ReactiveCocoa ](https://github.com/ReactiveCocoa/ReactiveCocoa) 从 5.0 开始，主要框架逻辑也已经全部由 swift 实现。ReactiveCocoa 与 RxSwift 编程模型最大的区别，是冷热信号由两种类型表示。



## 9. 音视频

Apple 自己提供了音视频处理框架 AVFoundation。开发者也有第三方开源框架可以选择，比如由法国程序员 Fabrice Bellard 使用 C语言编写的 **[FFmpeg](https://github.com/FFmpeg/FFmpeg)** ，B站开发的 Android/iOS 播放器框架 **[ijkplayer](https://github.com/bilibili/ijkplayer)** 就基于FFmpeg。



## 10. 其他

**[Dollar](https://github.com/ankurp/Dollar)** 是一个「标准库扩展」，类似于 Lo-Dash 或 Javascript中 的Underscore.js，它能够在不扩展任何内置对象的情况下，提供有用的函数式编程辅助方法。

这里涉及一个函数式编程里的概念：**柯里化**（Currying），即把一个多参数的函数拆分成一系列函数，每个拆分后的函数都只接受一个参数（unary）。



持续更新中，欢迎交流~

