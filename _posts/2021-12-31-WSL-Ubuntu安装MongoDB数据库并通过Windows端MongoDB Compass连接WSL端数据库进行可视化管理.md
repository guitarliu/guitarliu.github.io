---
layout: post
title: "WSL-Ubuntu安装MongoDB数据库并通过Windows端MongoDB Compass连接WSL端数据库进行可视化管理"
date: 2021-12-31
excerpt: "WSL-Ubuntu installs MongoDB and connects to the WSL DataBase through the Windows-side MongoDB Compass for visual management"
tags: [MongoDB Database, WSL, Ubuntu, MongoDB Compass]
comments: true
---




<figure align=center>
	<a href="https://pixabay.com/get/g5963dcafed70322f21052fa8b6c63dd3e1e31fb6230326b64fc25e9a55db65af48d07667a3cc010c6970f9e6a7af8bc21f3cb3ae571bf4d719aa3002e8adc18c34dec1bec610d9173184144a43750be9_640.jpg"><img src=https://pixabay.com/get/g5963dcafed70322f21052fa8b6c63dd3e1e31fb6230326b64fc25e9a55db65af48d07667a3cc010c6970f9e6a7af8bc21f3cb3ae571bf4d719aa3002e8adc18c34dec1bec610d9173184144a43750be9_640.jpg></a>
</figure>


##### 📌 首先安装MongoDB Shell
访问[MongoDB Shell](https://www.mongodb.com/try/download/shell)，选择Debian / Ubuntu 64-bit, deb格式，复制下载链接https://downloads.mongodb.com/compass/mongodb-mongosh_1.1.7_amd64.deb；<br>

进入WSL命令行

```
wget https://downloads.mongodb.com/compass/mongodb-mongosh_1.1.7_amd64.deb
sudo apt install ./mongodb-mongosh_1.1.7_amd64.deb
```
MongoDB Shell安装完毕。

##### 📌 安装MongoDB-server

访问[MongoDB Community Server](https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-server_5.0.5_amd64.deb)，选择Ubuntu 20.04，复制下载链接；<br>

进入WSL命令行

```
wget https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-server_5.0.5_amd64.deb
sudo apt install ./mongodb-org-server_5.0.5_amd64.deb
```
MongoDB-server安装完毕

##### 📌 安装MongoDB-Clients

```
sudo apt install mongodb-clients
```

##### 📌 安装MongoDB-Dev

```
sudo apt install mongod*
```
##### 📌 开启并连接数据库

1. 在dbpath路径下新建数据库目录文件

```
sudo vi /etc/mongodb.conf
```
查看dbpath路径，默认dbpath=/var/lib/mongodb；该路径可自定义；但是无论自定义与否，都要在dbpath已有路径下继续新建data/db子文件夹(命令如下)，这样mongodb才能正确连接。

```
sudo mkdir -p /var/lib/mongodb/data/db
```
2. 连接数据库

```
sudo mongod --dbpath /var/lib/mongodb/data/db
```

##### 📌 进入MongoDB Shell命令行

```
sudo mongosh
# 或者
mongosh
```

##### 📌 连接Windows端MongoDB Compass可视化工具

访问[MongoDB Compass](https://www.mongodb.com/try/download/compass)，下载MongoDB Compass工具包，解压后，运行MongoDBCompass.exe，在“Paste your connection string (SRV or Standard)”下方地址栏填入 【mongodb://[linux-ip-address]@127.0.0.1:27017】。

具体语法规则如下：

```
mongodb://[username:password@]host1[:port1][,...hostN[:portN]][/[defaultauthdb][?options]]
```
- wsl-Ubuntu IP地址可通过ifconfig命令查询eth0网卡IP获得。


