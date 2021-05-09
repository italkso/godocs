## CPU、多线程与 GCD

````Swift
// iOS 异步编程中常用(创建必须张贴所有UI代码的队列)
DispatchQueue.main.async {
	// 主队列
}

// 创建具有某种优先级的非 UI 队列
DispatchQueue.global(qos:.background).async {
    // 执行复杂任务
}
````

**GCD (Grand Central Dispatch，中央调度系统)**是对Grand Central Terminal的引用，作用是通过将工作提交由系统管理的调度队列，在多核硬件上同时执行代码。

一般GCD 会让所有代码在按其编写的先后**顺序 （Serial）** 运行。默认情况下代码都会被 GCD 放在**主队列 （main）**运行。

但如果所有业务都放在主队列，某些复杂业务可能会阻塞主队列。为此，GCD通过 **队列 FIFO** 和**线程池**，实现了任务的**并发（Concurrent）**执行。

 Swift 中默认提供的并发队列叫做**全局队列 （Global）**，全局队列使用参数 **QOS**（Quality of Service）考虑任务的优先级。

按优先级从高到底分别是：

- **`.userInteractive`** 

  快速执行此操作，决定UI。将 QOS 设置为 UI 级时GCD 会将任务分配到高性能核心上尽快完成。

- **`.userInitiated`** 

  用户发起的任务，现在就做

- **`.utility`** 

  需要发生，但非用户请求

- **`.background`** 

  后台任务，如清理等维护任务

线程池的管理由操作系统完成。GCD的工作方式是允许可并行运行的程序中的特定任务排队等待执行，并根据处理资源的可用性，安排它们在任何可用处理器内核上执行。线程（Threads）、队列（Queues）、闭包（Cloures）、主队列（Main Queue）：系统使用单个线程来处理主队列中的所有代码块。 因此，它也可以用于同步。后台队列（Background Queues）。

GCD 的两个基本任务是：

- 访问队列
- 将代码块放入队列



### 多线程

将一个闭包加入队列有 2 种基本的方式，最常用的是`.async`，它将在“稍后执行这个闭包”。在 UI 代码中不会调用.sync，因为它会阻塞 UI。但是，你可以在后台队列中调用它。

```Swift
// 将闭包加入队列的 2 种基本方式
let queue = DispatchQueue.main  // or DispatchQueue.global(qos:)
queue.async {/*在队列上执行的代码*/}
queue.sync {/*在队列上执行的代码*/}
```

嵌套（Nesting）：下面异步执行的代码似乎是同步的，但实际上不是。

```Swift
DispatchQueue(global: .userInitiated).async {
  // 执行可能会花费较长时间的任务
  // 不在主队列，所以不会阻塞 UI
  // 一旦完成了这一长期的工作，就可能需要更改UI
  // 但我们无法在此处执行UI，因为此代码是在主队列之外执行的
  // 所以，将需要的UI代码放入一个闭包中
  DispatchQueue.main.async {
    // 主队列，UI 代码可以执行
  }
}
```

异步 API：在 iOS 异步编程中常常使用 `DispatchQueue.main.async { }` ，而`Dispatch.global(qos:)`用得少，原因是大量异步 iOS API 运行在更高层次。大量 iOS 函数会在全局队列中自动完成他们的工作。比如 URLSession（从一个 URL 读取数据并返回）。

#### 数据结构和函数

`Dispatch`（调度）框架声明了几种数据类型和函数来创建和操作它们：

- **队列和任务**
  - `DispatchQueue`（调度队列）：一个对象，用于在应用程序的主线程或后台线程上串行或并发地管理任务的执行。
  - `DispatchWorkItem` （调度工作项）：  以某种方式封装想要执行的工作，从而可以附加  completion 句柄或执行依赖项。
  - `DispatchGroup` （调度组）： 将一组任务作为一个单元监视。
  - `DispatchQoS`：任务的服务质量或执行优先级。
- **系统事件监视**
  - `DispatchSource`  ：一个对象，用于协调处理特定的低级系统事件，例如文件系统事件，计时器和UNIX信号。
  -   `DispatchIO`  ：一个对象，使用基于流或随机访问的语义管理文件描述符上的操作。
  -   `DispatchData` ： 一个对象，用于管理基于内存的数据缓冲区，并将其公开为连续的内存块。
  -  `DispatchDataIterator`  ：调度数据对象内容上的逐字节迭代器。
- **任务同步**
  - `DispatchSemaphore`  ：一个对象，使用「计数信号量」控制对跨多个执行上下文的资源的访问。
- **Time Constructs**
  - `DispatchTime`：相对于默认时钟的时间点，纳秒精度。
  - `DispatchWallTime`：根据 wall clock 的绝对时间点，以微秒为单位。
  - `DispatchTimeInterval`：枚举，单位为秒，毫秒，微秒或纳秒。
  - `DispatchTImeoutResult`：表示调度操作是否在指定时间之前完成的结果值。
  - `dispatch_time_t`：时间的抽象表示。
  - `DISPATCH_WALLTIME_NOW: UInt`：当前时间。
- **Dispatch 对象**
  - `DispatchObject`  ：大多数 dispatch 类型的基类。
  -   `DispatchPredicate`  ：枚举，在给定执行上下文中进行评估的逻辑条件。
  -   `func dispatchPrecondition(condition: () -> DispatchPredicate)`  ：检查进一步执行所需的调度条件。