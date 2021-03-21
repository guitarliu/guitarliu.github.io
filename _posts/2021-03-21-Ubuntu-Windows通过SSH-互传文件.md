---
layout: post
title: "Ubuntu-Windows通过SSH互传文件"
date: 2021-03-21
excerpt: "Display ways to transport files between Ubuntu and Windows10 using SSH"
tags: [Ubuntu and Windows, SSH, File Transport]
comments: true
---

### ​​Ubuntu端安装并启动ssh服务:

~~~
sudo apt-get install openssh-server
sudo service ssh start
~~~

### Windows10端安装ssh服务:

Windows10端系统自带openssh服务，所以只需在命令行调用即可。如下图：

<figure>
    <a href="http://blog.askadc.com/wp-content/uploads/2020/04/check-openssh.jpg"><img src="http://blog.askadc.com/wp-content/uploads/2020/04/check-openssh.jpg"></a>
</figure>

### Windows10通过ssh连接Ubuntu服务器
    
~~~
ssh username@hostname -p port
~~~

- username为Linux端用户名

- hostname为Linux端IP地址，查找Linux端IP地址可用ifconfig；如果输入ifconfig报
- 错，说明Linux端未安装ifconfig，需要通过sudo apt-get install ifconfig 安装 ifconfig
- port为ssh端口，默认为22

### 上传Windows10文件至Linux端

- 上传Windows10桌面某一文件至Linux端某一文件夹处。打开Windows10终端，输入以下命令:

  ~~~
  scp c:/users/username/Desktop username@hostname:path/destination_filename
  ~~~

- 上述第一个username为Windows10的用户名，第二个username为Linux端用户名
  
- 如果需要上传文件夹至Linux端，只需在scp后面加一个 -r 即可，即：
  
  ~~~      
  scp -r c:/users/username/Desktop/test username@hostname:destination_dir
  ~~~

### 下载Linux至Windows10

- 下载Linux某一文件夹路径下某一文件至Windows10某一路径下（如桌面）

   - 打开Windows10终端，输入以下命令:
    
    ~~~    
    scp username@hostname:path/sourcefilename c:/users/username/Desktop
    ~~~  
    
    上述第一个username为Linux的用户名，第二个username为Windows10端用户名
  
    如果需要下载文件夹至Windows10，只需在scp后面加一个 -r 即可，即：

    ~~~
    scp -r username@hostname:path/source_dirname c:/users/username/Desktop
    ~~~
