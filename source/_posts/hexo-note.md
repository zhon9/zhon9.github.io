---
title: hexo note
date: 2019-09-10 14:43:04
tags: hexo
---
### 下载nodejs后
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install -g hexo-cli
```

### 下载项目文件
```bash
// 配置ssh-key
ssh-keygen -t rsa -C "your e-mail"

git clone -b hexo git@github.com:zhon9/zhon9.github.io.git
```

### hexo命令
```bash
// 写作 
hexo new post <title>

// 生成并部署
hexo g -d
```