# 快速上手

YiriMirai OneBot 需要 **Python 3.8 及以上版本**。

YiriMirai OneBot 需要一个 OneBot 11/12 的实现来为其提供服务，你可以在 [此处](https://onebot.dev/ecosystem.html) 找到 OneBot 的相关实现。

## 安装

我们还没有将YiriMirai OneBot发布到PyPI，但你可以从 Github 下载并安装本项目：

```bash
git clone https://github.com/YiriMiraiProject/YiriMiraiOneBot.git
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
bot = Bot(
    adapter=ReverseWebsocketAdapter(
        access_token='<此处填入访问 token>',
        host='0.0.0.0',
        port=8120,
        timeout=10  # 发送、接收的超时事件
    ),
    bot_platform="机器人平台"
    bot_user_id="机器人用户id"
)
```

其中，`bot_platform`和`bot_user_id`参数是可选的，但如果你的OneBot实现上托管了多个机器人账号，你应该设置他们，否则会出现一些奇奇怪怪的问题（雾

然后，我们来监听一些事件，并在回调函数中对它们进行处理。

```python
@bot.on(MessageGroupEvent)
async def handle_message_group(event: MessageGroupEvent):
    await bot.call(SendMessageRequest(
        params=SendMessageRequestParams(
            detail_type="group",
            group_id=event.group_id,
            message=MessageChain([
                Text('你好')
            ]).to_dict()
        )
    ), response_type=SendMessageResponse)
```

!!!warning
	不要漏掉`async`。

上文中，我们使用了`bot.call`函数来调用接口，这可能不太直观而且与其他OneBot SDK甚至YiriMirai的风格不太相同，但我推荐你这么做。

一方面，我们在开发中使用了`pydantic`库，因此你可以**方便地从 json 文档加载预设的动作组**，也可以**方便地保存动作组到 json 文档**。

其次，对于一些OneBot实现的专有接口，你可以直接定义数据模型来调用它们，而且可以获得`pydantic`提供的优秀类型提示、校验功能。

!!!note
	我们后续会提供一些常用接口的简化形式。