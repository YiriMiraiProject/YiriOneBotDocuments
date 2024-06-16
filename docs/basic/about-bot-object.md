# Bot 对象

!!!warning
	下文中的**OneBot 实现**、**Bot（机器人）**等词均按照 [OneBot 术语表](https://12.onebot.dev/glossary/) 解释。

Bot 对象是你在开发中打交道最多的对象之一。

Bot 对象表示一个**机器人实例**，你通过这个对象来和**OneBot实现**打交道，控制机器人执行操作。

## 创建 Bot 对象

Bot 对象接受的参数如下，其中必填项用**粗体**标识：

| 参数         | 作用                                                         |
| ------------ | ------------------------------------------------------------ |
| **adapter**  | 适配器，用于和**OneBot实现**通信。<br />常用的有`ReverseWebsocketAdapter`和`HTTPAdapter`。*目前我们仅实现了 `ReverseWebsocketAdapter`*。 |
| bus          | 一个事件总线，不填自动生成。<br />一般用于将多个 Bot 对象挂载到同一事件总线，这样它们的事件将在同一总线上传播。 |
| bot_platform | 一个字符串。**机器人平台**。用于筛选发给自身的事件，不填自动接收并处理所有 OneBot 实现上挂载的机器人的事件。 |
| bot_user_id  | 一个字符串。**机器人用户 ID**。用于筛选发给自身的事件，不填自动接收并处理所有 OneBot 实现上挂载的机器人的事件。 |

```python
bot = Bot(
    adapter=ReverseWebsocketAdapter(
        access_token='test',
        host='0.0.0.0',
        port=8120,
        timeout=10
    )
)
```

## 调用 API

你可以通过 `bot.call` 方法来调用任何一个 API。

`bot.call` 接收两个参数，`request` 参数用于构造一个**OneBot 请求**；`response_type` 用于指定返回值的类型，Bot 对象会根据 `response_type` 解析**OneBot 响应**。

!!!note
	得益于 `typing` 库的帮助，`await bot.call(...)` 的返回类型会被 IDE 自动推断为 `response_type`，因此你可以直接获得 IDE 提供的代码补全和 mypy 等工具的类型检查！
	![示例](https://xycode-blog-cdn-1302614822.cos.ap-hongkong.myqcloud.com/hexo/20240617010859.png)

除此之外，我们在后续版本中也会提供一些常用API的简化版本。