# 使用 RealityKit 构建空间体验

### RealityKit介绍
* 整合2D和3D混用
* 带入身临其境的体验中
* Apple核心3D框架，尤其vrOS

### RelityKit and SwiftUI
* Model3D很容易替换掉原有的Image
	* 异步加载后排版
	* 有占位生成器
* Model3D放置在最前面
	* window样式：.Volumetric
	* 保持真是的固定尺寸
	* 可以缩放下也保持真实
* Windows Group


### 实体，组件
* swiftUI中有两种使用RealityKit：
	* Model3D，RealityView
* Entity不能直接展示，需要通过加入Compnents
	* 材质组件
	* 变换组件 - transform component
		* 将实体放入3D空间中
		* 控制位置，方向，设置其属性以及设置父级来缩放
* 坐标空间
	* 单位是1米
	* RealityView有一个函数来回切换RealityKit和SwiftUI之间的坐标

* 每个实体都有一个变换，但并非每个实体都有模型。
* 有时，一个实体由多个子实体组装而成，每个子实体都有自己的一组组件。
`例如，您可以在子实体的变换上播放单独的动画。`

![01](./imgs/Build_compnents.jpeg)

### RealityView
* 是一个SwiftUIView，包含RealityKit的Entity
	* 只有加入到该View后，才能够渲染，动画，模拟等一系列行为。
* 通过update闭包关联SwiftUI中的state及参数
* 坐标转换：坐标点，边界框（bounding boxes）
* 订阅实体和组件发布的事件
* SwiftUI视图附加到实体中


### Input，动画，音频

