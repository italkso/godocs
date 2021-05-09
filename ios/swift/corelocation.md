## Core Location 地理位置信息框架

Core Location 框架提供一切与设备地理位置，海拔高度有关的信息。Core Location 会自动调用设备中的 GPS、网络、蓝牙、磁力计、气压计等硬件，并将上述硬件中的信息汇总。

开发者可以使用 Core Location 框架的 CLLocationManager 获取地理位置信息，使用 MapKit 中的 MKCoordinateRegion 将地理位置信息转化为一个可以显示的地理位置区域，用 Combine 框架中的 @Published 将数据更新推送给 SwiftUI。 



### 使用步骤

1. **向 Info.plist 增加描述，以向用户申请地理位置授权**

   访问用户隐私信息需要经过用户授权。向用户申请地理位置授权的方法是，打开应用中 Info.plist 文件，新增一个条目 「Privacy - Location When in Use Usage Description」。

2. **使用 Core Location 和 Combine 框架完善 ViewModel 逻辑，并提供对应数据**

   导入 Foundation、Combine 和 Core Location 等必要的框架，并完整处理逻辑。Foundation 框架负责提供 Swift 语言及常用功能。

3. **在 SwiftUI 中添加地图视图，以显示地理位置信息**

   导入地图框架[MapKit](https://developer.apple.com/documentation/mapkit) 和 UI框架 SwiftUI并制作地图显示界面。

   

### 代码

ViewModel 文件`LocationManager.swift`。

```swift
import Foundation
import CoreLocation
import Combine
import MapKit

class LocationManager: NSObject, ObservableObject, CLLocationManagerDelegate {
    
    let locationManager = CLLocationManager()
    @Published var region = MKCoordinateRegion(
        center: CLLocationCoordinate2D(
            latitude: 37.785834,
            longitude: -122.406417
        ),
        span: MKCoordinateSpan(
            latitudeDelta: 5,
            longitudeDelta: 5
        )
    )
    
    override init() {
        super.init()
        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.requestWhenInUseAuthorization()
        locationManager.startUpdatingLocation()
    }// Have to init in a class
    
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        guard let location = locations.last else { return }
        region = MKCoordinateRegion(
            center: CLLocationCoordinate2D(
                latitude: location.coordinate.latitude,
                longitude: location.coordinate.longitude
            ),
            span: MKCoordinateSpan(
                latitudeDelta: 5,
                longitudeDelta: 5
            )
        )
    }
}

```

说明：

- Core Location 框架使用中介 CLLocationManager 访问地理位置信息。 
- 将经纬度等变量设置为 @Published 以便在位置变化时进行更新。
- 需要继承 NSObject（历史原因）
- 遵循 ObservableObject 协议：让 LocationManager 能作为 SwiftUI 数据源使用
- 遵循 CLLocationManagerDelegate 协议：其中的`locationManager(_:didUpdateLocations:)`表示数据更新时需要做什么。
- 设备每次地理位置变化时，系统会通过 `locations.last` 将最新数据传递给开发者。



MyMapView.swift 文件：

```swift
import SwiftUI
import MapKit

struct MyMapView: View {
    @StateObject var locationManager = LocationManager()
    var body: some View {
        VStack {
            Map(coordinateRegion:$locationManager.region)
                .edgesIgnoringSafeArea(.all)
        }
    }
}
```



**Links**

[1] <https://developer.apple.com/documentation/corelocation>

