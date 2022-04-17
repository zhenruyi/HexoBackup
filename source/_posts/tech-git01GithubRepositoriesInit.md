---
title: Github仓库初始化
date: 2021-02-02 19:00:00
id: git1
categories:
- tech
tags:
- git
---



将Github的远程仓库和本地仓库关联起来。



<!-- more -->



```bash
…or create a new repository on the command line
echo "# SortingAlgos" >> README.md

# 初始化
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zhenruyi/SortingAlgos.git
git push -u origin main

…or push an existing repository from the command line
git remote add origin https://github.com/zhenruyi/SortingAlgos.git
git branch -M main
git push -u origin main

…or import code from another repository
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
```

