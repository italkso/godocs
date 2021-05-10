## App Tracking Transparency 是什么



> App Tracking Transparency ，是 Apple 最新推出的、旨在提升App 跟踪的透明度的框架。



2021 年 4 月 27 日，Apple 公司在 iOS 14.5 的正式推送中，iPhone 在菜单**`设置 > 隐私 > 跟踪`**里提供了一个是否「**允许 App 请求跟踪**」的开关， 默认设置是「关闭跟踪」。

Apple 提供的这项新功能提升了 App 跟踪的透明度。实际上，大部分用户都不愿意「用隐私换便利」。「用隐私换便利」这种说法背后，实则是用户的无奈。所以你可以看到，在 iOS 14.5 的正式推送后，很多 iPhone 用户都对 Apple 的举动表示了赞赏。

随着用户隐私意识的增强，一个应用如果在提供良好服务的同时，能够保证用户的隐私不被侵犯，那口碑自然也不会差。对于 iOS 开发者而言，尊重用户的隐私肯定是最好的选项。在这项新功能背后，所涉及的框架是 **App Tracking Transparency** 。AppTrackingTransparency 框架的作用是，**请求用户授权，获取对可用于跟踪用户或设备的应用程序相关数据的访问权限**。

如果你的应用收集了有关终端用户的数据，出于跨应用和对网站进行跟踪的目的与其他公司共享，那么你必须使用 AppTrackingTransparency 框架。 只有在用户授权后，你的应用才允许访问与应用程序相关的数据，并用于跟踪用户或设备。



## AppTrackingTransparency 框架使用步骤

使用 AppTrackingTransparency 框架的步骤如下：

1. **使用 `import AppTrackingTransparency `导入框架**

   导入框架才能使用。

2. **设置 `NSUserTrackingUsageDescription` 以显示系统权限请求弹窗**

   在 `info.plist` 中新增名为 `Privacy - Tracking Usage Description`的`property list key`，其值是一条消息，用于通知用户为什么应用程序正在请求许可以使用数据来跟踪用户或设备，比如 Allow tracking for better service。设置之后才能使用 `requestTrackingAuthorization（completionHandler :)`。

3. **调用方法 `requestTrackingAuthorization（completionHandler :)`将应用程序跟踪授权请求呈现给用户** 

   `requestTrackingAuthorization（completionHandler :)`是一项一次性请求，用于授权或拒绝对可用于跟踪用户或设备的应用程序相关数据的访问。 系统会记住用户的选择，并且不会再次提示，除非用户先卸载然后在设备上重新安装该应用程序。

   ```swift
   class func requestTrackingAuthorization(completionHandler completion: @escaping (ATTrackingManager.AuthorizationStatus) -> Void)
   ```

4. **使用属性 `trackingAuthorizationStatus` 确定应用程序跟踪许可权状态**

   ```swift
   class var trackingAuthorizationStatus: ATTrackingManager.AuthorizationStatus { get }
   ```

   `ATTrackingManager` 是提供跟踪授权请求和应用程序的跟踪授权状态的类 class，继承自类 `NSObject`。

   `ATTrackingManager.AuthorizationStatus`是应用程序跟踪授权的状态值，是一个枚举 enum。

   ```swift
   enum AuthorizationStatus : UInt {
       case authorized
       case denied
   	case notDetermined
   	case restricted
   }
   ```

   为了能够访问那些用于跟踪用户或设备的应用程序相关数据，应用需要向设备提出授权请求。设备收到授权请求后，返回值为：

   - `ATTrackingManager.AuthorizationStatus.authorized`（允许）
   - `ATTrackingManager.AuthorizationStatus.denied`（拒绝）

   设备未收到授权请求前的返回值为：`ATTrackingManager.AuthorizationStatus.notDetermined`。

   使用应用程序跟踪数据的授权受到限制时的返回值为：`ATTrackingManager.AuthorizationStatus.restricted`。



**Reference**

<https://developer.apple.com/documentation/apptrackingtransparency>

