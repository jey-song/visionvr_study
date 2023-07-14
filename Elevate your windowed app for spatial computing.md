# 将你的window升维到空间计算

## 宣传SwiftUI
* 加入visionOS平台

## 与iPadOS不同
* Glass背景
	* 内置控件新增了许多自动行为
* 动态内容缩放
	* 没有了带有物理像素的屏幕来定义。尽量不要使用固定尺寸的空间
	* 需要提供矢量assets
		* 位图在不降低质量时候无法缩放
		* xCode中替换为矢量图全平台都可用
* 背景色设置不能使用深色模式
	* Vibrant 
	* 使用语义填充颜色而不是使用纯色


## 交互
* 四种方式
	* 眼，手势，点击，辅助功能

* 眼睛的悬停效果hover
	`hoverEffect()`
* 为了隐私协议设计的悬停

### Layout
* 无尺寸概念
	* 考虑使用Tab View用于top-level窗口
		* tabbar位于左侧叫新名词Ornaments装饰品
	
	* Ornaments装饰品
		* 位于底部鸟缺水的装饰（类似推送UI）
		
		
### 总结：
* 为交互增加悬停效果
* 使用矢量图和Vibrant（语义填充颜色）更易看
* 增加装饰（Ornaments）用于辅助控制
