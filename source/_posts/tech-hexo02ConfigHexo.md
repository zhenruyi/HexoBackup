---
title: 配置博客信息
date: 2022-03-26 12:31:42
id: hexo2
categories:
- tech
tags:
- hexo
---

修改站点标题、关键字信息。

修改配置文件以修改站点信息，使用next主题美化站点，配置next主题，修改主题样式，添加站点logo，代码高亮显示。

<!-- more -->



#### 1 修改站点标题、关键字信息

修改根目录下的`_config.yml`文件，找到Site区域。

```yaml
# Site
title: zhenruyi #站点标题，标签上的
subtitle: 我们都在忍受着漫长 #副标题
description: 学习，工作，生活。 #描述
keywords: thinking #关键词
author: luyizheng
language: en
timezone: Asia/Shanghai
```

---

#### 2 修改主题

目前 Hexo 应用最多的主题是 Next 主题，它支持的插件和功能也极为丰富，配置了这个主题，博客可以支持更多的扩展功能。

##### 2.1 下载主题

```bash
cd blog
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

##### 2.2 修改主题

修改项目根目录下的 `_config.yml `文件，找到 theme 字段。

```bash
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```

---

#### 3 修改主题样式

修改 `themes/next/_config.yml `文件，找到scheme字段。

Muse：经典；Mist：Muse的紧凑版；Pisces：双列；Gemini：Prisces的紧凑版。

```yaml
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini

# Dark Mode
darkmode: false
```

---

#### 4 favicon

favicon 就是站点标签栏的小图标，默认是用的 Hexo 的小图标，如果我们有站点 Logo 的图片的话，我们可以自己定制小图标。

##### 4.1 获取图标

[https://realfavicongenerator.net](https://realfavicongenerator.net/)

##### 4.2 更换图标

图标下载下来之后把它放在 themes/next/source/images 目录下面。

然后在配置文件里面找到 favicon 配置项。

```yaml
favicon:
  small: /images/favicon/favicon-16x16.png
  medium: /images/favicon/favicon-32x32.png
  apple_touch_icon: /images/favicon/apple-touch-icon.png
  safari_pinned_tab: /images/favicon/safari-pinned-tab.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```

---

#### 5 avatar

作者的头像。找到avatar配置项。

```yaml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: #/images/avatar.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: true
  # If true, the avatar will be rotated with the cursor.
  rotated: true
```

---

##### 6 rss

博客一般是需要 RSS 订阅的，如果要开启 RSS 订阅，这里需要安装一个插件，叫做 hexo-generator-feed，安装完成之后，站点会自动生成 RSS Feed 文件，安装命令如下：

```bash
npm install hexo-generator-feed --save
```

在项目根目录下运行这个命令，安装完成之后不需要其他的配置，以后每次编译生成站点的时候就会自动生成 RSS Feed 文件了。

---

##### 7 code block

```yaml
codeblock:
  # Code Highlight theme
  # Available values: normal | night | night eighties | night blue | night bright | solarized | solarized dark | galactic
  # See: https://github.com/chriskempson/tomorrow-theme
  highlight_theme: galactic
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result.
    show_result: true
    # Available values: default | flat | mac
    style: mac
```

---

##### 8 back to top

```yaml
back2top:
  enable: true
  # Back to top in sidebar.
  sidebar: false
  # Scroll percent label in b2t button.
  scrollpercent: true
```

