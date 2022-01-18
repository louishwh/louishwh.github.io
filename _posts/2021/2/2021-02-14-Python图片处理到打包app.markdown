---
layout: post
title: Python图片处理到打包app
date: 2021-02-14 10:00:00 +0800
categories: 【图片处理】
tag: Python
---

### 需求介绍
- 从网页上下载数据
- 将数据根据模版生成图片
- 最后打包成一个app

### 工具库
- 拉取数据
	- requests
- 解析网页
	- BeautifulSoup4
- 图片处理
	- Pillow
- 打包app
	- py2app | pyinstaller

### 大致代码 