## Local Authentication

#### Info.plist 隐私访问请求设置

在 Info.plist 的空白区域右键点击，并选择「Add Row」，选中高亮的横行并输入 Privacy ，然后在 Xcode 自动联想出的所有需要授权的隐私请求中选择所需的那一个。比如需要 Face ID 授权，就选择「Face ID Usage Description」并添加相应的值，比如「Unlock your phone」。

修改 Info.plist 文件后，需要明确授权逻辑。你可以使用 [**本地身份认证 Local Authentication**](https://developer.apple.com/documentation/localauthentication/) 框架。LA 框架的作用是通过设备自带的身份验证工具，告知开发者是否是机主在使用设备。它只负责调用本地硬件验证身份，整个过程中无需网络连接。本地身份认证框架支持 iOS 和 macOS 系统，它会根据设备类型不同，自动调用设备具备的 Face ID 或 Touch ID。

LA 内置了识别失败的处理情况，当人脸识别失败两次过后，系统会自动触发密码解锁界面。

`MyReaderApp.swift`:

```swift
import SwiftUI
import LocalAuthentication

@main
struct MyReaderApp: App {
    @State var locked = true

    var body: some Scene {
        WindowGroup {
            Group {
                if locked {
                    Locked(authorize: authorize)
                } else {
                    Master().environmentObject(motionManager)
                }
            }
            .onAppear { authorize() }
        }
    }

    func authorize() {
        let context = LAContext()
        var error: NSError?

        // If the device support Face ID or Touch ID
        if context.canEvaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, error: &error) {
            context.evaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, localizedReason: "Unlock the App") { result, _ in

            }
        }

    }
}
```

`Locked.swift`:

```swift
import SwiftUI

struct Locked: View {
    let authorize: () -> ()

    var body: some View {
        VStack {
            Image(systemName: "lock.shield")
                .font(.system(.largeTitle, design: .rounded))
            Button(action: {
                authorize()
                Vibration.light.vibrate()
            }) {
                Text("Try Again").bold().padding()
            }
        }
    }
}
```
