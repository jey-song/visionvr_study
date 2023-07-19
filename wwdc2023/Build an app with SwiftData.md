# 使用 SwiftData 构建应用程序

### # 介绍
* 请先看“认识 SwiftData” wwdc23

### # SwiftData Model
* 使用@Model，已经实现了监听，codable等协议

##### 1. 夸
* 极少代码
* 自动关联依赖，自动更新
* 将模型的可变状态绑定到 UI 元素从未如此简单

### # 查询展示UI
* @Query包装的宏
	* 提供轻量级语法来配置排序、排序、过滤，甚至动画更改
* 给view提供数据
* 当数据更改时触发UI的更新，像state一样
* 一个view可以有多个@Query查询属性
* 在底层，它使用视图的模型上下文（ModelContext）作为数据源。
	* 设置 ModelContainer，任何应用程序都必须设置至少一个 ModelContainer。
	* ModelContainer创建整个堆栈
	* 一个view只能有一个modelContainer
	* 窗口及其视图将继承容器
	* 有些应用程序需要一些存储堆栈，并且它们可以为不同的窗口设置多个模型容器。
	* SwiftUI 还允许在视图级别进行精细设置

### # 创建更新
* 环境变量获取modelContext.insert(x)
* 不需要调用save即可
	* 极少数可以手动调用save
* 


### # Documents-base app

* SwiftData 文档是包：如果您使用“externalStorage”属性标记 SwiftData 模型的某些属性，则所有外部存储的项目都将成为文档包的一部分。