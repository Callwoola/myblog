---
layout: post
title: "osx-xcode-install"
date: 2015-12-08 22:12:09 +0800
comments: true
categories: homebrew,ruby,OSX
---

brew install 出现 configure: error: cannot run C compiled
=================

当brew install <software>
出现

> configure: error: cannot run C compiled 

是系统升级最新的 Mac OS X El Capitan.造成的,无法运行C编译的程序。


Solution:
查看log，发现这是Xcode的命令行工具造成的。

运行以下命令：

```bash
xcode-select --install
```

希望它可以为您节省几个小时的使用Google :)

