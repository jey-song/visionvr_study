# 通过推送通知更新实时活动

### # 服务器更新Live Activity

#### 1. 准备工作APNs连接
* APNs 引入了一种新的实时活动推送类型：liveactivity
* 此推送类型仅适用于具有基于令牌的 APNs 连接的服务器，不适用本地
* 修改您的应用程序，打开push功能需求，以便将您的实时活动配置为接收推送更新
* Activity代码打开token
* Push生命周期贯穿整个活动，使用Task处理Token(直接返回会获取到nil)

```
func startActivity(hero: EmojiRanger) throws {
    let adventure = AdventureAttributes(hero: hero)
    let initialState = AdventureAttributes.ContentState(
        currentHealthLevel: hero.healthLevel,
        eventDescription: "Adventure has begun!"
    )

    let activity = try Activity.request(
        attributes: adventure,
        content: .init(state: initialState, staleDate: nil),
        pushType: .token
    )

    Task {
        for await pushToken in activity.pushTokenUpdates {
            let pushTokenString = pushToken.reduce("") { $0 + String(format: "%02x", $1) }
            
            Logger().log("New push token: \(pushTokenString)")
            
            try await self.sendPushToken(hero: hero, pushTokenString: pushTokenString)
        }
    }
}
```

* 每个活动的推送令牌都是唯一的，因此对于用户启动的每个实时活动，跟踪它们非常重要。
* 应用程序将获得前台运行时来相应地处理它。
* 将新的推送令牌发送到服务器并使旧的推送令牌失效非常重要

#### 2. 发送推送
* 发送APNs http请求
	* APNs header
	* APNs payload

```
curl \
  --header "apns-topic: com.example.apple-samplecode.Emoji-Rangers.push-type.liveactivity" \  # 格式：<bundle-id>.push-type.liveactivity
  --header "apns-push-type: liveactivity" \ # 类型
  --header "apns-priority: 10" \ # 5~ 10,优先级低 ->高
  --header "authorization: bearer $AUTHENTICATION_TOKEN" \
  --data '{
      "aps": {
          "timestamp": '$(date +%s)', # 时间1685956000，系统使用时间戳来确保它始终呈现最新的内容状态。
          "event": "update",
          "content-state": {
              "currentHealthLevel": 0.941,
              "eventDescription": "Power Panda found a sword!"
          }
      }
  }' \
  --http2 https://api.sandbox.push.apple.com/3/device/$ACTIVITY_PUSH_TOKEN
```

* 调试更新失败
	* 保证curl执行成功
	* APNs 返回成功的响应，则可以使用控制台应用程序查看设备日志并尝试对问题进行分类。
	* 可能具有相关日志的进程有 liveactivitiesd、apsd 和 chronod。
	

#### 3. 更新优先级差异及提醒用户
* 低优先级
	* 保护电池，优先级传递
	* 可能不会立即更新
	* 好处是可以发送的更新数量没有限制
* 高优先级
	* 高优先级更新会立即交付
	* 电池寿命的影响
	* 如果应用超出预算，系统将限制您的推送更新
	* 为应用程序启用实时活动频繁更新功能
		* 向 Info plist 添加一个名为NSSupportsLiveActivitiesFrequentUpdates = YES
		* 用户可以在“设置”中独立于实时活动禁用频繁更新
		* 通过访问 ActivityAuthorizationInfofrequentPushesEnabled 属性来检测频繁更新功能的状态
		* 服务器应根据此值调整其更新频率，请确保在开始发送推送更新之前将其发送到服务器，只需在活动开始后检查该值一次。
		* 推送提示

``` 推送报警
{
    "aps": {
        "timestamp": 1685952000,
        "event": "update",
        "content-state": {
            "currentHealthLevel": 0.0,
            "eventDescription": "Power Panda has been knocked down!"
        },
        "alert": {
            "title": {
                "loc-key": "%@ is knocked down!",
                "loc-args": ["Power Panda"]
            },
            "body": {
                "loc-key": "Use a potion to heal %@!",
                "loc-args": ["Power Panda"]
            },
            "sound": "HeroDown.mp4"
        }
    }
}
```


### # 增强功能
* 通过发送推送有效负载并将事件设置为结束来完成此操作

```
{
    "aps": {
        "timestamp": 1685952000,
        "event": "end", // 结束
        "dismissal-date": 1685959200, // 可不设置，由系统控制
        "content-state": {
            "currentHealthLevel": 0.23,
            "eventDescription": "Adventure over! Power Panda is taking a nap."
        }
    }
}
```
* payload中添加了一个“过时日期”字段。系统将使用此日期来决定何时渲染陈旧视图。
* 具有更重要更新的内容应该位于顶部附近，而最重要的应该是在动感岛上。
* 可以通过提供可选的“relevance-score”字段来安排此操作。数字越高表示相关性越高。

[https://developer.apple.com/videos/play/wwdc2023/10185](https://developer.apple.com/videos/play/wwdc2023/10185)