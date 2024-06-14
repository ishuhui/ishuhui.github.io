---
title: Git常用命令
top_img: transparent
tags:
  - Git
abbrlink: 7065
date: 2022-05-14 16:34:31
---

# 确定分支

```bash
# 查看当前分支
git branch

# 切换分支
git checkout 分支名
```

# 创建文章

```bash
# 1.创建新文章
hexo new 文章名

# 2.更新文章
hexo clean && hexo g && hexo d
hexo clean; hexo g; hexo d

# 3.开启本地服务，在本地查看
hexo s

# 4.本地正确前往gitee更新
```

# 提交项目

```bash
# 初始化仓库（只初始化一次）
git init

# 添加文件到暂存区
git add .

# 提交
git commit -m "vue:todoList"

# 推送
git push

```

# 备份

```bash
# 1.切换到备份分支
git checkout beifen

# 2.添加文件到暂存区
git add .

# 3.提交
git commit -m "vue:todoList"

# 4.推送
git push
```

