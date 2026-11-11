# 链接下载视频技能

## 项目内容

- `SKILL.md` 是给 Codex 读取的技能说明。
- 本文件介绍工具、安装和使用方法。

本仓库不含视频、浏览器 Cookie、账号信息或下载程序。技能指导 Codex 调用本机工具完成任务，普通 ChatGPT 聊天能否运行取决于它是否连接了相应工具。

## 需要的工具

1. **Codex** 用于读取这个 Skill 和执行下载任务。
2. **yt-dlp** 用于解析和下载支持的视频链接。项目及安装方法见 [yt-dlp 官方仓库](https://github.com/yt-dlp/yt-dlp)。
3. **FFmpeg 和 ffprobe** 用于合并视频与音频、检查文件，以及在需要时制作字幕版。项目见 [FFmpeg 官网](https://ffmpeg.org/)。
4. **Deno 或 Node.js** 用于 yt-dlp 处理 YouTube 的部分 JavaScript 挑战。具体支持版本和设置见 [yt-dlp 官方指南](https://github.com/yt-dlp/yt-dlp/wiki/EJS)。
5. **浏览器** 用于查看视频，或在用户本人同意时处理网站验证。是否需要登录取决于视频和平台。

在已经安装 Homebrew 的 Mac 上，可参考以下命令安装工具。

```bash
brew install yt-dlp ffmpeg
```

安装完成后，用以下命令检查。YouTube 所需的 JavaScript 运行时及 EJS 组件请按上面的官方指南确认。

```bash
yt-dlp --version
ffmpeg -version
ffprobe -version
```

## 在 Codex 中使用

将仓库克隆到 Codex 的技能目录，再在新的 Codex 会话中使用。

```bash
git clone https://github.com/88480030/link-video-download-skill.git ~/.codex/skills/link-video-download
```

也可直接提供 `SKILL.md` 的路径。

发送视频链接并说：

> 使用链接下载视频技能，下载这个链接的视频，放到 ai视频学习文件夹。

需要字幕时可以补充：

> 使用链接下载视频技能，为这个视频添加简体中文字幕，并保留字幕文件。

默认使用当前工作区的 `ai视频学习/` 文件夹。你可以指定其他保存位置。

## 直接用命令行下载

把下面的示例链接替换成实际视频地址。这个示例下载单个视频，保存到当前目录下的 `ai视频学习`。

```bash
mkdir -p ai视频学习
yt-dlp --no-playlist -t mp4 -P ai视频学习 'https://www.youtube.com/watch?v=视频ID'
```

部分视频需要登录、验证或额外的 JavaScript 环境。`--cookies-from-browser` 可能读取整个浏览器配置文件中多个网站的 Cookie，因此使用前应确认授权范围，保护账号登录状态。macOS 若出现钥匙串提示，请由本人决定是否允许。

## 实际使用示例

本次用 yt-dlp 和 Chrome 中的 YouTube 登录会话下载成功，生成了 1080p 视频。中文字幕来自 YouTube 自动翻译，通过浏览器导出后用 FFmpeg 压入画面。字幕时间按整秒记录，部分专有名词可能有翻译错误。平台验证和下载能力可能随时间变化。
