# 网易云点歌（薇塔版）

基于 [NachoCrazy 的网易云点歌插件](https://github.com/NachoCrazy/netease-music-astrbot-plugin) 修改，提供搜索、选歌、歌曲信息、语音播放和音质回退，另有薇塔风格点评与歌曲记录

## 特性与使用限制

- 使用 `/点歌 歌名` 搜索，回复列表中的数字选歌，搜索结果有效期为 60 秒，也支持 `/music`、`/听歌`、`/网易云` 及部分自然语言点歌
- QQ OneBot 优先通过音频链接发送语音，减少 Base64 消息过大导致的失败。实际发送仍取决于音频链接、适配器和平台限制；非 QQ 平台沿用 AstrBot 的语音发送方式，尚未全面验证
- 播放后可调用当前会话的聊天模型生成薇塔风格点评，并可参考歌曲热门评论；模型不可用时回退到预设回复。点评仅参考文本，并非听过歌曲的评价
- 按群聊或私聊分别保存最近 50 条发送记录，后续请求可参考最近 5 条，以及最多 3 条与当前消息中歌名匹配的旧记录。仅记录启用后的内容，并不保证模型每次都准确回忆

## 安装与配置

1. 本版本在 AstrBot 4.29.4 环境测试；安装并运行 [Netease Cloud Music API 增强版](https://github.com/neteasecloudmusicapienhanced/api-enhanced)，确保 AstrBot 能访问该服务
2. 将本插件目录放入 AstrBot 的 `data/plugins` 目录，重载插件或重启 AstrBot。与原版插件同时启用可能重复响应，建议停用原版
3. 在插件配置中设置网易云 API 地址、优先音质、搜索数量，以及是否生成点评、参考热门评论
4. 当前插件会检查运行 AstrBot 的环境是否存在 FFmpeg；未找到时改发音频链接，请在运行环境中安装并配置 FFmpeg

## 数据与隐私

歌曲记录保存在 AstrBot 的插件数据目录下的 `song_history`，按会话隔离，包含时间、点歌人昵称、歌曲信息、发送方式和已发出的点评，每个会话最多保留 50 条；不保存音频链接或热门评论。删除该目录可清空歌曲记录

开启点评后，歌曲名称、歌手、专辑和最多 5 条热门评论内容会发送至当前聊天模型；不会主动附带评论者用户名或账号。评论文本本身可能包含个人信息，可在插件配置中关闭热门评论或关闭点评。后续聊天请求会向当前聊天模型提供同一会话的部分点歌记录

## 署名与许可

原作者为 [NachoCrazy](https://github.com/NachoCrazy)，原项目为 [netease-music-astrbot-plugin](https://github.com/NachoCrazy/netease-music-astrbot-plugin)。本版本由 M1steln 维护，保留原项目的 [MIT 许可证文本](LICENSE)
