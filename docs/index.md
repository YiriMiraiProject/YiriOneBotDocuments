# Welcome
此处是 YiriMiraiOneBot 的文档仓库。YiriMiraiOneBot 的代码仓库在 [此处](https://github.com/YiriMiraiProject/YiriMiraiOneBot)。

## 关于 YiriMirai OneBot

YiriMiraiOneBot 是一个 OneBot 12 协议上的 Python SDK，同时我们也在努力兼容 OneBot 11。它延续了 YiriMirai 项目轻量级、低耦合的编码风格。

尽管 YiriMiraiOneBot 中带有 Mirai 字样，但由于 OneBot 协议在多个平台上都有不同的实现，因此你也可以将其用于 [LagRange](https://github.com/LagrangeDev/Lagrange.Core) 等项目。并且，从 OneBot 12 开始，OneBot 标准不再与 QQ 紧耦合 ，而是适用于一切支持聊天机器人的地方，因此你也可以将本项目用于编写其他平台上的机器人。

!!!Warning
	YiriMiraiOneBot 正处于开发状态，请勿将其用于生产环境。

## 什么情况下该使用 YiriMirai OneBot

1. 你是 YiriMirai 的老用户
2. 你要经过

### 立即换用 YiriMirai OneBot！

如果你还在使用 YiriMirai，我们建议您**在近期**换用YiriMirai OneBot，主要有如下几点原因：

1. 原有的YiriMirai项目是与mirai-api-http项目绑定的，这意味着它无法在非mirai的平台上使用。
2. YiriMirai项目目前无人维护，我们不能保证其的稳定性和兼容性。
3. YiriMiraiOneBot有计划开发一个名为**YiriBot**的项目。<br>该项目对YiriMiraiOneBot进行了更高级的封装，提供了类似**FastAPI**和**Typer**的API供使用。