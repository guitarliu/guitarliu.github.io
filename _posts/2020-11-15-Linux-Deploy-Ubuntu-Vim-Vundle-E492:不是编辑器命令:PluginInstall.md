---
layout: post
title: "Linux-Deploy Ubuntu Vim Vundle-E492:不是编辑命令: PluginInstall"
date: 2020-11-15
excerpt: "Solutions about solving Vim Plugin bugs."
tags: [Linux-Deploy, Ubuntu, Vim, Vim Plugin]
comments: true
---

## Solutions
将.vimrc放在"~"目录下，新建同时在“~”目录下新建".vim"文件目录，将插件以及Vundle插件利用"git clone xxxxx.git"命令放置在.vim目录下；
在.vimrc文件中添加"Plugin xxx"后，退出编辑模式，输入":PluginInstall"安装所需插件，具体安装及配置详见各插件github页介绍。
