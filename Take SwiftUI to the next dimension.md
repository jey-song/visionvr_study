# swiftUI如何在新的维度中升级

### Volumes体积
* 没有主玻璃窗Glass window
* 使用现有的window代码创建，仅设置为3d的样式即可
* 提供等比例的容器，根据距离动态缩放

### 3DView和布局
* 加载3D资源
* 3DView加载类似AsyncImage
* phase指示加载状态
* 加载对其方式：默认后背平面对其back face alignment，修改为前面对齐：
	```.frame(depth: object.size, alignment: .front)```

### RealityKit 逼真的kit
* 详细："Enhance your spatial computing app with RealityKit." 和 "Build spatial experiences with RealityKit" 
* SwiftUI通过附件可以在RealityView中使用

### RealityView
* Components概念
* 添加手势
	* 指定特定Entity接收手势
	* 手势获取到的是location坐标
	* 坐标转换：location坐标转换为entity坐标
* 混合手势
	* 第二段代码

	
### 总结
* 强大的新类型场景
* 几何及布局
* 适用3D的RealityView介绍
* 手势使用

```swift
struct MoonView {
  var body: some View {
    Model3D(named: "Moon") { phase in
      switch phase {
      case .empty:
        ProgressView()
      case let .failure(error):
        Text(error.localizedDescription)
      case let .success(model):
        model
          .resizable()
          .scaledToFit()
      }
    }
  }
}
```

```
// Gesture combining dragging, magnification, and 3D rotation all at once.
var manipulationGesture: some Gesture<AffineTransform3D> {
    DragGesture()
        .simultaneously(with: MagnifyGesture())
        .simultaneously(with: RotateGesture3D())
        .map { gesture in
            let (translation, scale, rotation) = gesture.components()

            return AffineTransform3D(
                scale: scale,
                rotation: rotation,
                translation: translation
            )
        }
}

// Helper for extracting translation, magnification, and rotation.
extension SimultaneousGesture<
    SimultaneousGesture<DragGesture, MagnifyGesture>,
    RotateGesture3D>.Value {
    func components() -> (Vector3D, Size3D, Rotation3D) {
        let translation = self.first?.first?.translation3D ?? .zero
        let magnification = self.first?.second?.magnification ?? 1
        let size = Size3D(width: magnification, height: magnification, depth: magnification)
        let rotation = self.second?.rotation ?? .identity
        return (translation, size, rotation)
    }
}
```