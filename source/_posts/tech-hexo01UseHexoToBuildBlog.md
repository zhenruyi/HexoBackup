---
title: 使用Github搭建自己的博客
date: 2022-03-26 03:05:00
id: hexo1
categories:
- tech
tags:
- hexo
---

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

<!-- more -->

1. 安装node.js

   下载链接：[Node.js (nodejs.org)](https://nodejs.org/en/)

   LTS：Long Term Support，长期支持。node.js的版本更新很快，长期支持版本意味着稳定、可靠。关于版本，官网是这样介绍的：

   > Releases
   > Major Node.js versions enter Current release status for six months, which gives library authors time to add support for them. 
   > After six months, odd-numbered releases (9, 11, etc.) become unsupported, and even-numbered releases (10, 12, etc.) move to Active LTS status and are ready for general use. 
   > LTS release status is "long-term support", which typically guarantees that critical bugs will be fixed for a total of 30 months. 
   > Production applications should only use Active LTS or Maintenance LTS releases.

   主要的node.js版本会经过两个阶段

   - 当前(Current)版本状态，时长六个月，目的是给开发者时间添加支持；
   - 六个月之后
     - 奇数版本不再被支持
     - 偶数版本变成长期支持版本(LTS)，提供广泛使用，并支持30个月。

   ![](https://zhenruyi.github.io/images/01_nodejs_releases.png)

   测试是否安装成功：

   ```bash
   node -v
   ```

   ---

2. 安装git

   安装git并配置环境变量。成功配置后cmd输入：

   ```bash
   git --version
   ```

   ---

3. 新建GitHub仓库

   仓库名：账号名.github.io

   勾选`Add a README file`

   在setting中打开pages，看到仓库的域名，可以通过外网访问。

   ---

4. 安装hexo

   1 本地新建一个文件夹，命名为“blog”；

   2 在该文件夹打开cmd，输入`npm install hexo -g`。提示升级npm：` Run npm install -g npm@8.5.5 to update!`。

   3 输入`hexo -v`查看hexo版本。

   ---

5. 初始化hexo仓库

   1 输入`hexo init`初始化hexo。报错：

   ```bash
   ERROR Cannot find module 'hexo' from 'A:\CodeHub\blog'
   ERROR Local hexo loading failed in A:\CodeHub\blog
   ERROR Try running: 'rm -rf node_modules && npm install --force'
   ```

   原因：博客根目录下缺少node_module文件夹

   解决办法：hexo仓库不是空的，所以把hexo仓库内容删了，重新初始化。

   2 安装组件`npm install`
   
   ---

6. 使用hexo

   1 使用`hexo generate`将hexo编译生成HTML代码，在根目录的public目录下。

   2 在本地运行`hexo serve`，浏览器访问`http://localhost:400`

   3 假如页面无法跳转，端口被占用。输入`hexo server -p`指定端口号。
   
   ---

7. 将hexo和pages关联起来

   1 配置密钥，公钥给GitHub。

   2 找到_config.yml文件，修改repo值。

   ```yaml
   # Deployment
   ## Docs: https://hexo.io/docs/one-command-deployment
   deploy:
     type: git
     repo: git@github.com:zhenruyi/zhenruyi.github.io.git
     branch: main
   ```

   3 新建一篇post，`hexo new post "PostName"`。

   4 安装一个扩展`npm install hexo-deployer-git --save`

   5 `hexo d -g`生成以及部署
   
   ---

8. 其他分支

   ```bash
   那我博客的源码也想放到 GitHub 上面怎么办呢？其实很简单，新建一个其他的分支就好了，比如我这边就新建了一个 source 分支，代表博客源码的意思。
   
   具体的添加过程就很简单了，参加如下命令：
   
   git init    # 初始化项目
   git checkout -b source    # 创建并切换到source分支
   git add -A    # 添加所有文件到暂存区
   git commit -m "init blog"    # 提交并注释
   git remote add origin git@github.com:59devops/59devops.github.io.git    # 添加到远程仓库
   git push origin source    # 将代码提交到远程的source分支
   在GitHub仓库中可以看到已经有两个分支。
   ```

   