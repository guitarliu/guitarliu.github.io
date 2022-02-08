---
layout: post
title: "Ubuntu 点击声音按钮显示Establishing connection to PulseAudio. Please wait解决办法"
date: 2022-02-08
excerpt: "Solutions for Ubuntu of Clicking the sound button but showing 'Establishing connection to PulseAudio. Please wait'"
tags: [Ubuntu, Solutions, PluseAudio]
comments: true
---

##### :cookie: 首先，卸载原有pluseaudio, 并重装
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get remove --purge alsa-base pulseaudio
sudo apt-get install alsa-base pulseaudio pavucontrol
sudo alsa force-reload
reboot
```
##### :loudspeaker: 重启后运行如下命令
```
sudo apt-get install pavucontrol
sudo apt-get install pulseeffects
```

##### :repeat: 最后检查并启动 PulseAudio
```
pulseaudio --check
pulseaudio -D
```