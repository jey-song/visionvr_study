# 开始第一课：空间计算平台

# 穿透技术
passthrough

realitykit

arkit

skeletal hand tracking


基本的空间概念：
windows
volumes 体积
spaces

### 互动
1. 眼睛看，做简单手势
2. 现有手势在实际的虚拟空间点击
	* 原有的拖拽，缩等手势基本都支持
3. 骨骼手势
4. 无限鼠标
### n
5. group activity framework
6. 已经做了共享屏幕

### 关于隐私：
* 隐私第一
	* 禁止访问传感器内容
* 组织数据和交互
	* 系统会提供事件和提示
		* 用户的眼睛和位置，会作为触摸事件传送
		* 用户注意力窗口，系统会有悬停效果，但不会告知在哪里看什么
* 清楚的权限要求

### 怎么开发

* xcode
	* 现有的画布已经支持RealityKit 的3d代码，包括动画和自定义代码
	* 扩展后可支持许多运行时的可视化，根据简单提示处理错误
* 性能提高，原有的instruments
	* RealityKit Trace
	* Reality Composer Pro
		* Preview
		* Prepare
	* 新功能particles
		* 添加颗粒，可提供转移，生命，云雨火花等效果
		* 有标准的材料，音频具有空间特效
		* 材料可与背景联系
		* 额外标准材料使用开源MaterialX来编写
	* 无需接触代码，窗口快速预览
	* 无需开发，可以在设备预览
	* 详细参考：“Meet Reality Composer Pro”

* Unity

### 怎么开始
* 新app
	* 根据xCode的模块来
		* 选择windows或立体的
		* 选择公共空间或者Full Space
	* 例子
		* Destination Video: 3D音视频
		* Happy Beam：沉浸空间有戏，自定义手势，可以和朋友一起
		* Hello World：3D地球仪，视觉模式转换
		
		```
		从头开始构建app，了解空间计算的概念
		```
		
* 现有的App
	* 可以旋转，拉伸
	* xCode中添加支持设备即可

### Hello World
* Window
	* 使用SwiftUI展示
	* 支持2D和3D内容混合展示
	* 可以缩放和切换位置
	
	* Model3D：由RealityKit渲染
	* 手势:
		* 现有的
		
		```
		* tap  * spatial tap点击 * 拖拽 * 放大 * 旋转 * 长按 * onHover悬停 *  onContinuesHover  * keyboardShortcut   * onKeyPress
		```
		
		* 新的3D手势
		
		```
		* 3D旋转  * 3D轻拍等
		```
		
* Volumes体积容器
	* Extension of a Window
	* Ideal for 3D content风格很适合3D内容
	* 该主机可容纳多个Views：2D和3D均可以
	* 为共享空间创建
	
	* RealityView
		* 举例......
		* 详细在："Build saptial experiences with RealityKit"  and "Enhance your spatial computing app with RealityKit"

* FullSpace
	* 专注于app
	* Place app content anywhere
	* 更多样性的自定义交互
	* 与周围环境交互
	* 不同层次的沉浸感
	* 更多学习："Meet ARKit for spatial computing"

* 沉浸感immersion style：
	* mixed
	* progessive
	* full



	