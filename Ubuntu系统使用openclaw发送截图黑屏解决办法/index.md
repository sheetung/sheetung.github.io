# Ubuntu系统使用openclaw发送截图黑屏解决办法


## 问题原因

在 Wayland 显示协议下，使用 `scrot` 等 X11 截图工具会导致黑屏。原因是 Wayland 对屏幕捕捉有更严格的安全限制。

## 可能遇到的问题

- `scrot` 截图黑屏
- `grim` 报错：`compositor doesn't support wlr-screencopy-unstable-v1`

## 🛠️ 解决方案

### 1. 安装截图工具

安装 Wayland 兼容的截图工具：

```bash
sudo apt-get update && sudo apt-get install -y grim slurp
sudo apt-get install -y gnome-screenshot
```

> `grim` 和 `slurp` 用于部分 Wayland compositor；`gnome-screenshot` 适用于 GNOME 环境。

### 2. 截图命令

**方式一：gnome-screenshot（推荐 GNOME 用户）**

```bash
gnome-screenshot -f /home/sheetung/.openclaw/workspace/current_screen.png
```

**方式二：grim（需要 compositor 支持 wlr-screencopy）**

```bash
grim /home/sheetung/.openclaw/workspace/current_screen.png
```

### 3. 配置 mediaLocalRoots 允许访问本地目录

配置 OpenClaw 允许访问需要的本地目录，才能发送截图文件：

**允许访问 workspace 目录**

```bash
openclaw config set channels.feishu.mediaLocalRoots '["/root/clawd"]'
```

**或者同时允许 /tmp（用于临时文件）**

```bash
openclaw config set channels.feishu.mediaLocalRoots '["/root/clawd", "/tmp"]'
```

### 4. 重启 gateway 使配置生效

```bash
openclaw gateway restart
```

## 环境信息

- 系统版本：Ubuntu 24.04.2 LTS
- 显示协议：Wayland
- 验证可用：`gnome-screenshot`


---

> 作者: 西塘  
> URL: https://sheetung.github.io/Ubuntu%E7%B3%BB%E7%BB%9F%E4%BD%BF%E7%94%A8openclaw%E5%8F%91%E9%80%81%E6%88%AA%E5%9B%BE%E9%BB%91%E5%B1%8F%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%95/  

