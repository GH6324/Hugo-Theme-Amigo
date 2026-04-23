# Amigo - 极简朋友圈风格 Hugo 主题

[![Hugo](https://img.shields.io/badge/Hugo-%230076D1.svg?style=flat&logo=hugo&logoColor=white)](https://gohugo.io/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Amigo 是一款为 [Hugo](https://gohugo.io/) 打造的极简博客主题，其设计灵感来源于 **微信朋友圈 (WeChat Moments)**。它旨在提供一个私密、亲切且易于阅读的动态分享空间，支持 PJAX 无刷新加载和多种评论系统。

[English Documentation](./README_EN.md)

---

## ✨ 主题特性

- 📱 **朋友圈 UI**：高度还原微信朋友圈视觉体验，支持九宫格图片展示。
- 🚀 **全站 PJAX**：丝滑的无刷新页面切换，提升浏览体验。
- 🌓 **深色模式**：支持手动切换及系统跟随。
- 💬 **多评论系统**：内置 **Artalk / Twikoo / Giscus** 三种评论方案。
- 🖼️ **图片灯箱**：集成 ViewImage.js，点击图片即可放大浏览。
- 🎨 **精美排版**：本地化中文字体优化（内置 *zql* 字体），阅读体验更佳。
- 🛠️ **响应式设计**：完美适配手机、平板及桌面端。
- 🔙 **智能页眉**：滚动自动切换背景及显示标题，集成返回顶部功能。
- 🔍 **搜索功能**：支持本地搜索，无需依赖外部服务。
- 📍 **地点信息**：可在文章元数据中添加地点信息，展示在文章底部。

## 📸 预览站点

您可以访问 [Amigo 主题演示站点](https://www.200181.xyz) 来查看 Amigo 主题的实际效果。

该站点已配置好所有必要参数，您可以直接浏览和评论。

## ⚙️ 前置条件

在开始使用 Amigo 之前，建议先准备好以下环境与服务：

- **Hugo 版本**：建议使用 Hugo 0.128.2版本，以确保兼容性和最佳体验。
- **Artalk**: 推荐使用2.8.7 版本，以支持朋友圈风格的点赞和评论功能
  artalk 文档地址：https://artalk.js.org/zh-CN/docs/quick-start，
  推荐使用官方提供的 `artalk/artalk:2.8.7` 镜像，确保与主题兼容，命令如下：
  ```bash
  docker run -d \
      --name artalk \
      -p 3378:23366 \
      -v $(pwd)/data:/data \
      -e "TZ=Asia/Shanghai" \
      -e "ATK_LOCALE=zh-CN" \
      -e "ATK_SITE_DEFAULT=你的站点名称" \
      -e "ATK_SITE_URL=你的站点URL" \
      artalk/artalk-go:2.8.7
  ```
- **Twikoo**: 推荐使用Twikoo EO版本，项目地址：https://github.com/Mintimate/twikoo-eo
- **Giscus**: 推荐使用最新版本，文档地址：https://giscus.app/zh-CN
- **浏览器**：建议使用现代浏览器（如 Chrome、Firefox、Edge）以获得最佳体验。

### 评论方案选择和作者建议

如果您有自己的服务器，**建议使用Artalk评论方案**

**因为Twikoo程序没有提供较为完善的Api，固会有一些功能上的缺失，如点赞，弹幕等**

如果您没有自己的服务器，**建议使用Twikoo评论方案**

因为Twikoo的EO版本支持部署在Edgeone平台，在国内有较好的访问速度

Twikoo EO版本，项目地址：https://github.com/Mintimate/twikoo-eo

**Artalk：**
- 已经部署好的 Artalk 服务端（支持 HTTPS 访问）。
- 在 Artalk 后台创建好对应的「站点」，并记住 `site` 名称。

**Twikoo：**
- 任选一种部署方式：
  - 腾讯云环境：已创建的环境 ID（`envId`）。
  - Vercel / 自建服务：可公网访问的后端地址，例如 `https://twikoo.your-domain.com`。
- 确保后端允许当前博客域名访问（CORS / 反向代理已配置好）。

**Giscus：**
- 一个启用 Discussions 功能的 GitHub 仓库。
- 在 [giscus.app](https://giscus.app) 中生成完整配置，包括：
  `repo`、`repoId`、`category`、`categoryId` 等字段。

准备好以上条件后，再根据下文配置对应的参数即可正常使用评论与主题功能。

## 🚀 快速开始

### 1. 安装

在您的 Hugo 站点目录下执行：

```bash
git clone https://github.com/zqlit/Hugo-Theme-Amigo.git themes/Amigo
```

### 2. 配置

您可以直接参考并复制主题目录下的 [hugo.toml](./hugo.toml) 文件到您的站点根目录。

或者将以下基本配置添加到您的 `hugo.toml` 中：

```toml
theme = "Amigo"

[params]
  # 基础信息
  username = "您的昵称"
  avatar = "/images/avatar.jpg"
  description = "一句话简介"
  cover = "/images/header.png" # 首页封面（图片）
  
  # 顶部封面也可以使用视频（与 cover 二选一）
  # headerMedia = "/images/header.png"
  # headerMedia = "/videos/2792755201.mp4"
  
  # 评论模式: "artalk"、"twikoo"、"giscus" 或 "none"
  commentMode = "artalk"

  # 字体设置: "ZQL", "PingFangQiaoMuTi", "AlimamaFangYuanTi"
  fontFamily = "ZQL"

  # --- 功能开关 ---
  showTags = true         # 是否显示文章标签
  showLocation = true     # 是否显示地点信息
  enableSearch = true     # 是否开启搜索功能
  enableDarkMode = true   # 是否显示深色模式切换按钮
  enablePjax = true       # 是否开启 PJAX 无刷新加载
  enableLightbox = true   # 是否开启图片灯箱

  # Artalk 配置
  artalkServer  = "https://your-artalk-server.com"
  artalkSite    = "您的站点名称"
  enableDanmaku = true   # 底部弹幕：true 开启、false 关闭
  
  # Twikoo 配置（任选其一）
  # 腾讯云环境：填 envId
  # twikooEnvId = "your-twikoo-env-id"
  # Vercel / 自建：填后端地址
  # twikooEnvId = "https://twikoo.your-domain.com"
  twikooLang = "zh-CN"

  # Giscus 配置（在 https://giscus.app 生成）
  giscusRepo             = ""
  giscusRepoId           = ""
  giscusCategory         = ""
  giscusCategoryId       = ""
  giscusMapping          = "pathname"
  giscusStrict           = "0"
  giscusReactionsEnabled = "1"
  giscusEmitMetadata     = "0"
  giscusInputPosition    = "bottom"
  giscusLang             = "zh-CN"
  giscusLoading          = "lazy"
  
  # 功能开关
  enablePjax     = true  # 开启 PJAX 无刷新跳转
  enableLightbox = true  # 开启图片灯箱放大查看
```

### 3. 详细配置说明

以下配置项可在主题自带的 [hugo.toml](./hugo.toml) 中找到完整示例：

#### 站点基础信息

- `username`：显示在头像右侧的昵称，默认也用作文章作者。
- `avatar`：头像图片地址，支持本地路径和外链。
- `description`：个人简介，显示在头像下方。
- `cover`：首页顶部封面图片。
- `headerMedia`：首页顶部媒体资源，可为图片或视频（与 `cover` 二选一）。
- `favicon`：浏览器标签页图标。
- `footerText`：页面底部文本，支持 HTML。
- `icp`：ICP备案号（可选）。

#### 评论系统

通过 `commentMode` 切换评论系统：

- `commentMode = "artalk"`：启用 Artalk 评论。
- `commentMode = "twikoo"`：启用 Twikoo 评论。
- `commentMode = "giscus"`：启用 Giscus 评论。
- `commentMode = "none"`：关闭评论。

> 注意：如果同时配置了 Artalk 与 Giscus，优先使用 Artalk；Twikoo 与它们互斥，由 `commentMode` 决定。

**Artalk 相关：**

- `artalkServer`：Artalk 后端地址，例如 `https://artalk.your-domain.com`。
- `artalkSite`：Artalk 中「站点名称」，用于区分多站点。
- `enableDanmaku`：是否开启底部弹幕（仅首页使用 Artalk 时有效）。

**Twikoo 相关：**

- `twikooEnvId`：
  - 腾讯云：填写环境 ID，例如 `yourid-xxxxxx`。
  - Vercel / 自建：填写后端地址，例如 `https://twikoo.your-domain.com`。
- `twikooLang`：Twikoo 语言，如 `zh-CN`。

**Giscus 相关：**

所有字段均可在 [Giscus 配置页面](https://giscus.app) 生成：

- `giscusRepo` / `giscusRepoId`
- `giscusCategory` / `giscusCategoryId`
- `giscusMapping`：评论与页面映射方式，一般使用 `pathname`。
- `giscusLang`：界面语言。

#### 字体与功能

- `fontFamily`：`"ZQL"`, `"PingFangQiaoMuTi"`, `"AlimamaFangYuanTi"` 三选一。
- `enablePjax`：是否开启 PJAX 无刷新跳转。
- `enableLightbox`：是否开启图片灯箱。

#### 导航菜单

导航采用 Hugo 标准菜单配置，在根 `hugo.toml` 中配置：

```toml
[[menu.main]]
  name = "首页"
  url  = "/"
  weight = 1

[[menu.main]]
  name = "关于"
  url  = "/about.html"
  weight = 2

[[menu.main]]
  name = "友链"
  url  = "/friends.html"
  weight = 3
```
## 📝 使用指南

### 目录结构

```text
content/
├── posts/           # 朋友圈动态 (文章)
├── about.md         # 关于页面
└── friends.md       # 友链页面 (layout: "friends")
```

### 撰写动态 (Posts)

在 `content/posts/` 目录下创建目录（Page Bundles）或直接创建 `.md` 文件。为了更好地管理图片，建议为每篇动态创建一个文件夹：

```markdown
---
title: "周末去爬山"
date: 2026-02-20
author: "Vaica"
location: "武汉·东湖"
---

今天天气真好，去公园散步，看到了好多花开了。🌸 

![春日1](photo1.jpg)
![春日2](photo2.jpg)

#生活 #春天 #摄影
```

### 常用 Shortcodes

Amigo 内置了一些好用的 Shortcodes，方便你在文章中插入特殊内容。

#### 实况照片 (Live Photo)

想要在博客里展示像 iPhone 实况照片一样的效果？用这个：

```markdown
{{< livephoto image="cover.jpg" video="video.mp4" >}}
```

- `image`: 封面图（静止时显示的图片）
- `video`: 视频文件（动起来的内容）

> 💡 小技巧：如果是同名的 `.jpg` 和 `.mp4` 文件（例如 `my-cat.jpg` 和 `my-cat.mp4`），你可以只写 `image="my-cat.jpg"`，主题会自动去找对应的视频文件。

---

### 评论开关逻辑

- **文章 (Posts)**：默认开启评论。设置 `comments: false` 可关闭。
- **静态页面 (Pages)**：默认关闭评论。设置 `comments: true` 可开启（如留言板）。

> 评论系统的实际类型由全局 `commentMode` 决定，支持 Artalk / Twikoo / Giscus。

### 友链配置

在站点根目录创建 `data/friends.yml`：

```yaml
- name: "Vaica"
  url: "https://usj.cc"
  avatar: "https://github.com/zqlit"
  description: "开发者"
```

然后在 `content/friends.md` 中设置：

```markdown
---
title: "友链"
layout: "friends"
---
```

## 🛠️ 技术栈

- **SSG**: [Hugo](https://gohugo.io/)
- **Icons**: [Remix Icon](https://remixicon.com/)
- **Comments**: [Artalk](https://artalk.js.org/) / [Giscus](https://giscus.app/)
- **JS Components**: ViewImage.js, PJAX.js

## ☕ 请我喝杯咖啡

如果你觉得这个主题还不错，欢迎请作者喝杯咖啡，支持后续的开发维护！

<table>
  <tr>
    <td align="center">
      <img src="https://usj.cc/image/reward/new.png" alt="微信赞赏" width="200" /><br />
      微信支付
    </td>
    <td align="center">
      <img src="https://usj.cc/image/reward/alipay.jpg" alt="支付宝" width="200" /><br />
      支付宝
    </td>
  </tr>
</table>

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 协议。

---

感谢使用 **Amigo**！如果您喜欢这个项目，欢迎点一个 **Star** ⭐️。


