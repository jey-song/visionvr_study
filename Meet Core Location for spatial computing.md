# 了解空间计算的 Core Location

### 怎么用
* CLLocationUpdate.liveUpdates
* 等待返回

* 应用程序在访问位置等敏感信息之前必须请求用户的许可
* 请求许可信息在info.plist配置
* 获取坐标

### 精确度
* 类似mac，大约100米
* 获取iPhone在附近一起更精准，iPhone 相同的水平

### 活跃App获取位置
* 应用程序在不运行时将无法获取位置更新
* 非活跃只有几秒
* 两个app重叠都可以获取到定位
* 并排两个，高亮哪个就可以获取定位
