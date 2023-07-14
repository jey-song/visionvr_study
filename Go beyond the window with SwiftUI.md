# 虚拟现实的开端

### 介绍Space
* 怎么开始使用
* 怎么显示content
* managing你的Space
* 自定义

### Space开始
* app同时只能打开一个Space
* 共享空间和沉浸空间
* Space的原点在用户的下方接近脚的位置

### 显示内容

* 使用3D的RealityView异步展示
* 将展示元素的RealityView作为ARKit的锚点
* 与SwiftUI坐标系的不同
	* SwiftUI: y指向下方，z是指向自己
	* RealityView：y指向上方
* 展示了空间和launchWindow混用
	* 涉及到启动和消失的两个api

### 管理Space
* Space的不同阶段，活跃，非活跃，后台
	* 随时可能切换为不活动的Space
	* 处理非活动时状态处理
* 坐标系
	* Immersive Space坐标系
	* 使用几何读取器，封装到上下文中了。proxy.transform
	* SharePlay中多个沉浸空间 -- "Build spatial SharePlay experiences." （会议等场景）
		* 空间原点会被移动到共享位置
* Immersive Style
	* Mixed
	* Progressive
	* Full

* 高级功能
	* 启动空间立即为沉浸式
		* 需要plist中两个配置 1. xxxSessionRole 2. xxxImmersionStyle
	* 设置暗效果，preferredSurroundingEffects
	* upperLimbVisibility 修改器的passthrough控制完全沉浸式的空间中隐藏实体手，替换为虚拟形象
* 虚拟肢体（手）
	* SpaceGloves
		* 相关章节："Evolve your ARKit app for spatial experiences." 


### 地址

https://developer.apple.com/videos/play/wwdc2023/10111/?time=868