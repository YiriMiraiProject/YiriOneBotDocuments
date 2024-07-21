# 快速上手

Yiri OneBot 需要 **Python 3.8 及以上版本**。

Yiri OneBot 需要一个 OneBot 11/12 的实现来为其提供服务，你可以在 [此处](https://onebot.dev/ecosystem.html) 找到 OneBot 的相关实现。

## 安装

我们还没有将Yiri OneBot发布到PyPI，但你可以从 Github 下载并安装本项目：

```bash
git clone https://github.com/YiriMiraiProject/YiriOneBot.git
poetry install
```

## 编写第一个机器人

!!!先决条件
   	1. **【必须】**有一定的Python基础。
      	2. **【必须】**遇到不懂的先看文档，如果还不能解决再提Issue！
         	3. **【必须】**会部署你需要的OneBot实现！以下是一些OneBot实现的文档，请自行查阅它们。<br>[Lagrange.OneBot](https://lagrangedev.github.io/Lagrange.Doc/Lagrange.OneBot/Config/) &ensp; [A-kirami/matcha](https://github.com/A-kirami/matcha/)
            	4. **【推荐】**一定的英语水平。（实在不行自己用翻译软件）
               	5. **【推荐】**一定的 Linux 基础。
                  	6. **【推荐】**了解 Python 异步编程。

首先，我们要创建一个机器人实例。

```python
bus = EventBus()
bot = Bot(
    adapter=ReverseWebsocketAdapter(
        host="127.0.0.1", port=8080, access_token="helloworld", bus=bus
    ),
    self_id=3442852292,
)
```

其中，`bot_platform`和`bot_user_id`参数是可选的，但如果你的OneBot实现上托管了多个机器人账号，你应该设置他们，否则会出现一些奇奇怪怪的问题（雾

然后，我们来监听一些事件，并在回调函数中对它们进行处理。

```python
@bus.on(GroupMessageEvent)
async def on_group_message(event: GroupMessageEvent) -> None:
    await bot.adapter.call_api(
        SendGroupMessageInterface,
        SendGroupMessageParams(
            group_id=event.group_id, message=MessageChain([Text("Hello World!")])
        ),
    )
```

!!!warning
	不要漏掉`async`。

上文中，我们使用了`bot.call`函数来调用接口，这可能不太直观而且与其他OneBot SDK甚至Yiri的风格不太相同，但我推荐你这么做。

一方面，我们在开发中使用了`pydantic`库，因此你可以**方便地从 json 文档加载预设的动作组**，也可以**方便地保存动作组到 json 文档**。

其次，对于一些OneBot实现的专有接口，你可以直接定义数据模型来调用它们，而且可以获得`pydantic`提供的优秀类型提示、校验功能。

一些常用接口有简化形式，例如发送消息：

```python
await bot.send_group_message(group_id=..., message=...)
await bot.send_private_message(user_id=..., message=...)
```