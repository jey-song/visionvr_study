# Meet RealityKit Trace

### RealityKit渲染
* 渲染包括 App进程，渲染服务器，合成器
* 渲染在共享空间，和Full Space是有区别的
	* 共享时受到渲染服务器渲染其他应用的影响
	* 共享应用同时提交信息到渲染服务器做处理，统一生成渲染帧
	
### 分析空间App
* 工具名称：RealityKit Trace
* 渲染帧
	* 每一帧的渲染时间，流畅标准90fps
	* 每一帧都有渲染的截止日期
		* 很好渲染，绿色
		* 勉强渲染，橙色
		* 超时丢弃的帧，红色
* CPU，GPU工作时间
* 在考虑Core Animation统计数据
	* 透明和模糊效果耗资源Transparency and Blur
	* 渲染通道的数量取决于核心动画必须为整个图像单独渲染的层数。
	* 还有银幕外的传球。离屏渲染

#### 1. SwiftUI的绘制优化
* 离屏渲染
	* 渲染在屏幕外但不展示
	* 在3D应用尤其重要，持续渲染，比如摇头
		* 阴影、遮罩、圆角矩形和视觉效果
	* 保持高效的静态UI
* 学习参考技术讲座："Demystify and eliminate hitches in the render phase." 
* 阴影和透明度结合，开销非常大

#### 2. 优化asset绘制
* 检查3D渲染中三角形，顶点绘制调用过多
* 检查优化静态资源Reality Composer Pro
* 参考：Meet Reality Composer Pro

#### 3. 降低系统功耗
* 确保Reality Metrics统计符合预期
* 使用Time Profile检查CPU情况
* 使用 Instruments 中的 Metal System Trace 模板来查看 GPU

### 优化的正式建议
#### Profile SwiftUI content
* SwiftUI instrunments
* CoreAnimation instrunments
* Hangs instrunments   相关："Analyze hangs with Instruments."

#### Profile 3D Asset
* Time Profiler for asset loading
* RealityKit Metrics for asset rendering
* Check assets using Reality Composer Pro

### Profile Metal content
* Use Metal System Trace template
	* 处理GPU相关

