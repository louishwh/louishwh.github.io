---
layout: post
title:  【工具】Sublime Text
date:   2019-02-10 23:50:00 +0800
categories: 工具
tag: 工具箱
---

### 用Sublime Text的理由

1. 轻量级的编辑器
2. 很简单的连接编译器/解释器
3. 配置简单
4. 插件也很多
5. 用起来很顺手

### Sublme Text的安装

[下载Mac版](https://download.sublimetext.com/Sublime%20Text%20Build%203176.dmg)

### Sublime Text包的安装

[安装过程](https://packagecontrol.io/installation)

手动导入Package Control:

1.Perferences > Browse Packages

2.将[Control.sublime-package](https://packagecontrol.io/Package%20Control.sublime-package)复制到 Installed Packages/

3.重启Sublie Text

### Sublime Text插件的安装

1. Command + Shift + P
2. Package Control: Install Package
3. 看到左下脚：等号在左右移动（在加载仓库）
4. 输入仓库名称即可


推荐仓库：
> [markdown](https://blog.csdn.net/qq_20011607/article/details/81370236)


### Sublime Text 集成编译器/解释器

1.Tools -> Build System -> New Build System

2.添加下列编程语言的配置

[Python](https://blog.csdn.net/qq_33304418/article/details/63337602)
> { 
	"shell_cmd": "python3  \"$file\"",  
	"encoding": "utf-8",
	"file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",    
	"env": {"LANG": "en_US.UTF-8"}
 }

Perl
> {
    "cmd": ["perl", "$file"],
    "file_regex": ".* at (.*) line ([0-9]*)",
    "selector": "source.perl",
    "encoding": "UTF-8"
}

Julia
> {
	"shell_cmd": "/Applications/Julia-1.0.app/Contents/Resources/julia/bin/julia \"$file\""
  }

3.添加前缀保存

4.运行前选择： Tools -> Build System -> X语言

5.Command + B即可运行

