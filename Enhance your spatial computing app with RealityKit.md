# Enhance your spatial computing app with RealityKit

### RealityKit都有啥
* 快看2019年的wwdc啥都有
* RealityView是SwiftUI和RealityKit间的桥梁

### 新功能附件
* 附件从SwiftUI嵌入到RealityKit中
* 添加view，执行创建，更新

### VideoPlayerComponent，视频播放
* 文件 -> AVPlayer -> VideoPlayerComponent -> 网格（可拖动）
* 支持2D，3D视频	
* 字母由AVPlayer提供并由VideoPlayerComponent自动显示
* 视频初始高度是1米

### Passthrough tinting
* 要使用直通着色，可以将isPassthroughTintingEnabled 属性设置为 true。

### Portals and worlds
* World是包含真实的要展示的系统内容
	* 相关文档：“探索空间计算渲染”
* 门户包括了
	* 包含了World，所以world还能在打开大门后可见
	* 模型组件包含两个属性：网格和材质。 mesh
	* 做法：
		* 创建ParticleTransitionSystem 的自定义系统。
		* updateParticles 
		
### 锚点
* 锚点将内容放到相关位置
* 两种跟踪模式：连续，一次
	* 定位后是否持续跟踪。
* 首先自己是一个点、面、投影等
* 把自己放置到场景中
* 还要有锚点标定物

### 总结
RealityView 中的附件允许您将 SwiftUI 内容嵌入到实体层次结构中，以便您可以将 UI 元素与 3D 元素并排放置。

VideoPlayerComponent、门户和粒子效果可让您添加动态元素以增强 RealityKit 中的场景。

最后，锚点可让您将 3D 内容附加到现实世界的表面，例如地板或墙壁。

“使用 RealityKit 构建空间体验”会议讨论了实体、组件和 RealityView 等关键概念。

“在 Xcode 中使用 Reality Composer Pro 内容”课程将带您完成使用 Reality Composer Pro 和 RealityKit构建沉浸式应用程序的过程。
