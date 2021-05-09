## iOS 存储：Core Data & CloudKit

使用 CoreData 框架实现本地存储需要准备 Model、ViewModel ，并展示在 UI 界面山。

### 准备 Model

1. 新建 Core Data 的 Data Model（数据模型模版） 文件

2. 新增实体（Add Entity）

   点击 Add Entity 新增实体，一个名为 Default 的 Configuration将会被自动创建，作用是用来设置对应的实体。当你需要设置 CloudKit 云存储开发，选中 Default 后在右侧面板中勾选「Used with CloudKit」即可。

3. 新增属性

   点击 Attributes 下的「+」即可新增属性，目的是告知数据库每个实体中应包含的数据。



### 准备 ViewModel

创建文件 CloudData.swift

```swift
import CoreData

struct MyReaderData {
    
    // 自身初始化
    static let shared = MyReaderData()		
    
    //	准备容器
    let container: NSPersistentContainer
    
    //	初始化容器
    init(inMemory: Bool = false) {
        container = NSPersistentContainer(name: "MyReader")
        //  检查内存中是否已存在数据库，并在必要时加载
        if inMemory {
            container.persistentStoreDescriptions.first!.url = 		
            URL(fileURLWithPath: "/dev/null")
        }
        container.loadPersistentStores(completionHandler: {_,_ in})
    }
}
```

NSPersistentConatiner 是一个支持本地存储的数据库容器。

如果需要支持本地和网络存储的**数据库容器 Container**，请使用`NSPersistentCloudKitConatiner` 。`NSPersistentCloudKitConatiner` 的默认类型为**private**，即每个用户仅能存取用户自己放入的数据，同一应用中的不同用户的数据不互相共享。

`NSPersistentCloudKitConatiner` 是一个非即时同步 API（ sync when its convenient），即时同步推荐使用 CloudKit 框架。

 

### 准备 View

包括创建用于展示的View，实现存储逻辑，读取并展现结果。

```swift
@Environment(\.managedObjectContext) var viewContext
@FetchRequest(sortDescriptors: [NSSortDescriptor(keyPath: \Entity.timestamp, ascending: false)], animation: .default)
    var checkIns: FetchedResults<Entity>
    
func createNewItem() {
    let newItem = Entity(context: viewContext)
    newItem.timeStamp = Date()
    newItem.longitude = locationManager.region.center.longitude
    newItem.latitude = locationManager.region.center.latitude
    try? viewContext.save()
}
```

上述代码用于在收到该环境的子视图中直接读取数据库容器的值。在 Core Data 中，数据库容器  包含一个实	体属性 [viewContext](http://s://developer.apple.com/documentation/coredata/nspersistentcontainer/1640622-viewcontext) ，其类型是[NSManagedObjectContext](https://developer.apple.com/documentation/coredata/nsmanagedobjectcontext)，作用是代为执行 container 的操作。

- 读取数据库

  使用属性包装器 [@FetchRequest](https://developer.apple.com/documentation/swiftui/fetchrequest) 自动向数据库发出读取请求，并将所得结果复制给 `FetchedResults`类型的变量中。

### 添加 iCloud Capability

如果有云同步需求，可以添加 iCloud Capability。方法如下：

选择项目 - 目标 Targets - iOS 应用，接着点击 「Capability」 来添加需要用到三个**能力 Capability**：

-  iCloud - 告知操作系统应用需要用到 iCloud 同步，请在设置中开启本应用对 iCloud 的使用权限。
- Push Noticification - 跟随 iCloud 权限自动加入，负责在云端数据发生变化时通知设备更新本地数据。
- Background Modes - 负责让应用在后台时，依旧允许数据更新。