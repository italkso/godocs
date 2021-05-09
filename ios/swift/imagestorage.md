## 图片存取概述

1. **将图片作为独立数据单独存储，并在 JSON 文件中存储图片数据的本地链接**

   这是常见的本地图片存储方式。使用 JSON 文件存储「图片名称及扩展名」，因为当 JSON 文件仅包含文本信息时读取很快，但在 JSON 文件中存储大量图片并不合适，所以使用本地磁盘存储「图片本身」。

2. **注意沙盒地址**

   图片实际地址是「沙盒地址 + 图片名称及扩展名」。在图片或其他文件的本地存取时，不要存储带沙盒链接的完整地址，存储名称即可。因为沙盒地址不固定，在应用安装、更新时都有可能改变。沙盒地址的改变会间接导致图片的完整链接地址改变，从而让应用因为找不到文件而报错。（`0A8B9F60-CEF4-44DB-891D-54A21452515A`）

3. **UIImage**

   `import SwiftUI`或 `import UIKit`后，就可以直接调用图片类型 `UIImage`。

   

4. **从系统相册中选择图片**

   将属于 UIKit 框架的图片选择器 [UIImagePickerController](https://developer.apple.com/documentation/uikit/uiimagepickercontroller) 与SwiftUI 集成，或者使用封装好的 SwiftUI 第三方库 [ImagePickerView](https://github.com/ralfebert/ImagePickerView)，以便用户能够选择系统相册中的图片来添加。

5. **将图片存储在本地磁盘**

6. 修改视图

7. 用 SwiftUI 视图将图片读取显示出来



### 图片存取

1. **在 Model 中新增变量**

   添加一个名为 `imageURLAppendix` 变量以存储图片的名称及扩展名。

2. **在 ViewModel 中增加存取逻辑**

   **读取图片**：提供图片地址参数 ；判断链接地址中是否有数据；如果取得图片数据则创建一张图片并返回。

   ```swift
   func getImage(_ imageURLAppendix: String) -> UIImage {
       let url = TabNoteData.sandboxURL.appendingPathComponent(imageURLAppendix)
       let imageData = try! Data(contentsOf: url)
       return UIImage(data: imageData, scale: 0.5)!
   }
   ```

   **存储图片**：将数据存储至沙盒中。存储图片时，你可以通过 GCD 将图片存储工作放置在后台线程中，即 `DispatchQueue.global(qos: .userInitiated).async`。

   ```swift
   func saveImages(id: UUID, data: Data) {
       DispatchQueue.global(qos: .userInitiated).async {
           let url = TabNoteData.sandboxURL.appendingPathComponent("\(id).png")
           try? data.write(to: url)
       }
   }// Save Images with GCD
   ```

   

### 图片选择

你可以通过将属于 UIKit 框架的图片选择器 [UIImagePickerController](https://developer.apple.com/documentation/uikit/uiimagepickercontroller) 与SwiftUI 集成在一起，以便用户能够选择系统相册中的图片来添加。

在 SwiftUI 中，你也可以使用封装好的 SwiftUI 第三方库 [ImagePickerView](https://github.com/ralfebert/ImagePickerView)。

- 添加变量

  `@State var image: UIImage?`图片预览

  `@State var showImagePicker = false` 记录图片选择器是否弹出

- 新增图片按钮`Button()`

- 



**Reference**

[1] <https://developer.apple.com/documentation/uikit/uiimage>



