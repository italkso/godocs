## Core Motion

### 使用 Core Motion 的准备

传感器框架 Core Motion 不需要用户确认即可访问传感器信息。

为了使用 Core Motion，需要定义数据结构，获取传感器信息，并做初始化。

```swift
import SwiftUI
import CoreMotion

class MotionManager: ObservableObject {
    let motionManager = CMMotionManager()

    @Published var x: CGFloat = 0
    @Published var y: CGFloat = 0
    @Published var z: CGFloat = 0

    init() {
        motionManager.startDeviceMotionUpdates(to: .main) { data, _ in
            guard let tilt = data?.gravity else { return }
            self.x = CGFloat(tilt.x)
            self.y = CGFloat(tilt.y)
            self.z = CGFloat(tilt.z)
        }
    }
}
```

注：CM 是 Core Motion 框架的缩写，CGFloat 开头的 CG 代表 Core Graphics 框架。

### 向 SwiftUI 视图中添加传感器反馈

手机的传感器信息可以作为整个应用的共享知识，放置在 MyApp.swift 中，作为一个环境变量来提供数据。

```swift
import SwiftUI

@main
struct MyApp: App {
    // MARK: - CoreMotion
    let motionManager = MotionManager()

    var body: some Scene {
        WindowGroup {
            Master().environmentObject(motionManager)
        }
    }
}
```

在需要使用的视图里接收 MyApp 传递下来的传感器信息：

```swift
@EnvironmentObject var motion: MotionManager
```
