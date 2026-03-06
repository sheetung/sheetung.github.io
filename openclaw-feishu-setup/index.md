# OpenClaw 与飞书的搭建始末


不知道赶没赶上这口热乎的，自己也是折腾了很久。从刚开始的 Clawbot，又到 Moltbot 然后是现在的 OpenClaw，应该是不会改名了吧！

也算是更新了有几个月？在安装的成功率和使用体验上都有了不小的进步。虽然目前博主也还没探索出更好玩的技能，但是对于搭建上还是有着不少经验（折腾过好几次也是~~）

所以本文会介绍 OpenClaw 的安装到与飞书的消息渠道的链接。

<!--more-->

## 0. 准备阶段

1. 一台服务器/个人电脑，配置要求并不高
2. 系统方面因为在终端/命令行中完成，所以 Linux/Win/Macos 都是可以的
3. 半个小时的个人时间

## 1. 安装 OpenClaw

此处其实可以参照官方教程，官方教程也是有中文版的。

如果你是 Linux/Macos 使用如下命令一键安装：

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

如果你是 win 操作系统，在 PowerShell/cmd 中：

```bash
iwr -useb https://openclaw.ai/install.ps1 | iex
```

当然还有 Docker 或者源码等安装方法，👉 [OpenClaw官方中文网站](https://docs.openclaw.ai/zh-CN/install)

如果出现安装失败，首要考虑网络问题。请在系统或者终端处打开代理，重新运行安装脚本。

## 2. 配置 OpenClaw

默认情况下安装成功会自动进入配置处理，如果没有可以手动进入配置，建议新开一个终端，输入以下命令进入配置项：

```bash
openclaw onboard --install-daemon
```

命令执行后会有类似如下显示，此处弹出免责声明，务必使用键盘控制选择 **yes**。

![](/assets/openclaw-feishu-1.png)

第一次配置，建议选择 **QuickStart**，快速体验：

```bash
Onboarding mode
│  ● QuickStart (Configure details later via openclaw configure.)
│  ○ Manual
```

如果已经进行过相关配置，会提示你对于已存在的配置项做什么处理，因为我已经安装过，我这里选择 **Use existing values**：

```bash
◆  Config handling
│  ● Use existing values
│  ○ Update values
│  ○ Reset
```

### 2.1 大模型配置

接下来就会来到模型的配置页面，官方预制了一些模型供应商，如果是第一次体验又不想麻烦可以选择 **GitHub/z.ai**，当然如果你的服务器并不在国内或者你有代理的能力，可以选择 **Gemini** 等。

国内也有很不错的模型供应商，这里以硅基流动的 GLM5 模型为例。

可以白嫖部分额度的大模型供应商：

1. 硅基流动，注册即送 14 元代金券 👉 [硅基流动](https://cloud.siliconflow.cn/i/ebbhNO28)
2. 白山智算，限时赠送 450 代金券 👉 [白山智算](https://ai.baishan.com/auth/login?referralCode=3ssWcDyFj4)

如果要使用自定义模型，控制光标到 **Custom Provider**，首先就会来到模型请求地址的配置。查看供应商的请求文档可知：

- 硅基的请求 url 为：`https://api.siliconflow.cn/v1`
- 白山的请求 url 为：`https://api.edgefn.net/v1`

```bash
◆  API Base URL
│  http://127.0.0.1:11434/v1█
└
```

填写完 url 需要配置 API Key，从各自的个人中心处增加 key，并选择 **Paste API key now** 配置：

```bash
◇  API Base URL
│  https://api.edgefn.net/v1
│
◆  How do you want to provide this API key?
│  ● Paste API key now (Stores the key directly in OpenClaw config)
│  ○ Use external secret provider
└
```

然后就是兼容接口的选择，这里建议选择兼容更好的 `OpenAI-compatible`。（大佬们轻喷，此处我不熟悉他们各有的区别于特色）

```
◆  Endpoint compatibility
│  ● OpenAI-compatible (Uses /chat/completions)
│  ○ Anthropic-compatible
│  ○ Unknown (detect automatically)
└
```

然后就是模型选择，目前市面上最好的肯定还是 **Anthropic** 团队的 **claude opus 4.6**，但是面对龙虾这个 token 饕餮，还是有些消费不起。所以可以退而求其次，重在体验，目前我认为最优解应该是智谱的 GLM5。

- 硅基的 GLM5 模型名字为：`Pro/zai-org/GLM-5`
- 白山的 GLM5 模型名字为：`GLM-5`

配置完成后会弹出一个命名框，这里建议在后面加上模型的名字，方便后续使用命令 `/model` 进行模型切换。填写完成后，**Model alias** 默认即可：

```bahs
◆  Endpoint ID
│  custom-api-edgefn-net-glm5█
└
```

### 2.2 飞书消息渠道配置

```bash
◆  Select channel (QuickStart)
│  ○ Telegram (Bot API)
│  ○ WhatsApp (QR link) (not linked)
│  ○ Discord (Bot API)
│  ○ IRC (Server + Nick)
│  ○ Google Chat (Chat API)
│  ○ Slack (Socket Mode)
│  ○ Signal (signal-cli)
│  ○ iMessage (imsg)
│  ● Feishu/Lark (飞书)
│  ○ Nostr (NIP-04 DMs)
│  ○ Microsoft Teams (Bot Framework)
│  ○ Mattermost (plugin)
│  ○ Nextcloud Talk (self-hosted)
│  ○ Matrix (plugin)
│  ○ BlueBubbles (macOS app)
│  ○ LINE (Messaging API)
│  ○ Zalo (Bot API)
│  ○ Zalo (Personal Account)
│  ○ Synology Chat (Webhook)
│  ○ Tlon (Urbit)
│  ○ Skip for now
```

因为本文以飞书为例，所以就使用飞书作为消息渠道。这里先不急选择飞书，我们在网页端完成飞书平台的配置。

以下内容来自[飞书 - OpenClaw](https://docs.openclaw.ai/zh-CN/channels/feishu)

#### 1. 打开飞书开放平台

访问 [飞书开放平台](https://open.feishu.cn/app)，使用飞书账号登录。选择创建企业自建应用，填写应用名称和描述，选择应用图标。

![](/assets/openclaw-feishu-2.png)

#### 2. 获取应用凭证

在应用的 **凭证与基础信息** 页面，复制：

- **App ID**（格式如 `cli_xxx`）
- **App Secret**

> 请妥善保管 App Secret，不要分享给他人。

![](/assets/openclaw-feishu-3.png)

#### 3. 配置应用权限

在 **权限管理** 页面，点击 **批量导入** 按钮，粘贴以下 JSON 配置一键导入所需权限：

![](/assets/openclaw-feishu-4.png)

```json
{
  "scopes": {
    "tenant": [
      "aily:file:read",
      "aily:file:write",
      "application:application.app_message_stats.overview:readonly",
      "application:application.self_manage",
      "application:bot.menu:write",
      "cardkit:card:write",
      "contact:user.employee_id:readonly",
      "corehr:file:download",
      "docs:document.content:read",
      "event:ip_list",
      "im:chat",
      "im:chat.access_event.bot_p2p_chat:read",
      "im:chat.members:bot_access",
      "im:message",
      "im:message.group_at_msg:readonly",
      "im:message.group_msg",
      "im:message.p2p_msg:readonly",
      "im:message:readonly",
      "im:message:send_as_bot",
      "im:resource",
      "sheets:spreadsheet",
      "wiki:wiki:readonly"
    ],
    "user": ["aily:file:read", "aily:file:write", "im:chat.access_event.bot_p2p_chat:read"]
  }
}
```

#### 4. 启用机器人能力

在 **应用能力** > **机器人** 页面：

1. 开启机器人能力
2. 配置机器人名称

![](/assets/openclaw-feishu-5.png)

此时来到 OpenClaw 配置处，选择飞书渠道，然后系统会自动安装飞书插件，待安装完成后提示输入，顺序不要搞反！
- **App Secret**
- **App ID**

配置完成后会来到技能页面的选择，此时我们回到飞书配置处。

#### 5. 配置事件订阅

> [!IMPORTANT]
> ⚠️ **重要提醒**：在配置事件订阅前，请务必确保已完成以上步骤。

在 **事件订阅** 页面：

1. 选择 **使用长连接接收事件**（WebSocket 模式）
2. ③处添加事件：`im.message.receive_v1`（接收消息）

![](/assets/openclaw-feishu-5.png)

#### 6. 发布应用

1. 在 **版本管理与发布** 页面创建版本
2. 提交审核并发布
3. 等待管理员审批（企业自建应用通常自动通过）

## 2.3 后续但重要的配置

此处 skill 技能等配置可以选择 skip 进行跳过，后面并一直选择默认即可。

如果您使用的是自选大模型供应商，那么就需要来到 **openclaw.json** 配置大模型的上下文窗口和输出长度。

对于 Linux 和 win 用户，openclaw 配置文件存在于用户目录下，即：

- Linux -->> `/home/<username>/.openclaw/openclaw.json`
- Win -->> `C:\Users\<username>\.openclaw\openclaw.json`

找到我们的模型相关的配置，对于参数大模型供应商都有标注，像白山的 GLM5 上下文就是 200K，**contextWindow** 就修改为：`200000`，一般 **maxTokens** 此处可以默认，如果后续遇到龙爪输出卡住的情况，可以稍微增加。

修改完成后保存：

```json
"models": {
  "mode": "merge",
  "providers": {
    "custom-api-edgefn-net-m2-5": {
      "baseUrl": "https://api.edgefn.net/v1",
      "apiKey": "sk-",
      "api": "openai-completions",
      "models": [
        {
          "id": "GLM5",
          "name": "GLM5 (Custom Provider)",
          "reasoning": false,
          "input": [
            "text"
          ],
          "cost": {
            "input": 0,
            "output": 0,
            "cacheRead": 0,
            "cacheWrite": 0
          },
          "contextWindow": 16000,
          "maxTokens": 4096
        }
      ]
    }
```

因为当我们在 2.2 处配置结束后，OpenClaw 就会默认启动，我们这里修改了大模型的配置信息，需要重启一次 OpenClaw：

```bash
openclaw gateway restart
```

更多内容参考官方 install 部分。

到这里，你应该可以从飞书唤醒 OpenClaw 了，恭喜你，尽情的使用吧。

> 我要把 OpenClaw 夸成翘嘴


---

> 作者: 西塘  
> URL: https://sheetung.github.io/openclaw-feishu-setup/  

