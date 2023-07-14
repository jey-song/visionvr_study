# 认识用于空间计算的 ARKit

### 基本api概念，构建块
* 提供Swift 和 C语音
* 灵活组合使用来实现功能
* 隐私优先进行保密访问数据

#### 1. 三个基本块组成
* ARKitSession
* DataProvider
* Anchor

#### 2. 数据和用户App之间有隐私隔离
* 传感器探测到的数据供ARKit守护进程处理

#### 3. 访问数据
* 用户App使用数据需要用户的同意
* 进入一个Full Space
	* ARKit不会发送数据到Share Space空间
* Auth Type：.worldSensing, .worldTracking

### World跟踪
* 6个自由度移动跟踪锚点
* WorldTrackingProvider功能
	* 添加锚点
	* 自动保存锚点，重启和启动可保留，重新编译安装的时候可以轻松删除
	* 获取设备姿势相对app的起始
	* 捕获设备的姿势
		* The device relative to the app's origin
		* 查询姿势是一个比较昂贵的操作
		* 主要是提供给开发者处理他们拥有的渲染

```
代码展示了怎么获取姿势，有个类似时间切面的概念，根据渲染时间获取到姿势
```

### 场景理解

* Plane detection平面监测
	* 提供出PlaneAnchor
	* 基本的平面几何图形（例如地板或墙壁）
* mash tranking
	* MashAnchor
	* 提供好多实体的类型
	* 顶点、法线、面和语义分类
* image tracking
	* ImageAnchor

### 手势追踪
* HandArchors形式提供给app
	* 骨架
	* 原点，HandAnchor 的变换是手腕相对于应用程序原点的变换
* chirality手性：确定左手还是右手
* 关节：可通过名称查询，关节包括其父关节
* root关节，local关节等节点结构
* 使用时可分为：
	* poll for latest HandArchors
	* 在锚点可用时异步接收它们
* 展示使用代码

搞了例子：
