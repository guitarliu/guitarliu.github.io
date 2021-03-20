### 更换ubuntu 20.04版本软件源

    sudo nano /etc/apt/sources.list

将原有deb源全部注释掉（前方加一个#即可），然后将下面的源粘贴到文本最后：

    deb <http://mirrors.aliyun.com/ubuntu/> focal main restricted universe multiverse
    deb-src <http://mirrors.aliyun.com/ubuntu/> focal main restricted universe multiverse
    deb <http://mirrors.aliyun.com/ubuntu/> focal-security main restricted universe multiverse
    deb-src <http://mirrors.aliyun.com/ubuntu/> focal-security main restricted universe multiverse
    deb <http://mirrors.aliyun.com/ubuntu/> focal-updates main restricted universe multiverse
    deb-src <http://mirrors.aliyun.com/ubuntu/> focal-updates main restricted universe multiverse
    deb <http://mirrors.aliyun.com/ubuntu/> focal-proposed main restricted universe multiverse
    deb-src <http://mirrors.aliyun.com/ubuntu/> focal-proposed main restricted universe multiverse
    deb <http://mirrors.aliyun.com/ubuntu/> focal-backports main restricted universe multiverse
    deb-src <http://mirrors.aliyun.com/ubuntu/> focal-backports main restricted universe multiverse

ctrl + x 退出编辑并保存。

### 更新软件源

    sudo apt update
    sudo apt upgrade

### 查看 Ubuntu IP地址

Linux终端命令行输入 ifconfig 即可。如果提示找不到命令（实际如果找不到该命令，会在报错信息中提示安装 net-tools），在Linux终端输入 sudo apt-get install net-tools 即可。

### 步骤一、安装xfce软件包

    sudo apt install xfce4

### 步骤二、安装xubuntu软件包

    sudo apt install xubuntu-desktop

### 安装xrdp允许远程连接

    sudo apt-get install xrdp

### 配置xrdp（配置端口）

    sudo sed -i '/sport=3389/g' /etc/xrdp/xrdp.ini

### 向xsession中写入xfce4-session

    sudo echo xfce4-session >~/xsession

### 重启xrdp服务

    sudo service xrdp restart

### 通过Windows远程桌面功能连接Linux

计算机: Linux IP地址:3389
点击连接，输入Linux用户名和密码

### 设置中文界面

    language-pack-zh-hans 简体中文

    language-pack-zh-hans-base

    language-pack-zh-hant 繁体中文

    language-pack-zh-hant-base

- 安装中文语言包

      sudo apt-get install  language-pack-zh-han*

- 运行语言支持检查
  
      sudo apt install $(check-language-support)

- 修改语言配置文件

      sudo nano /etc/default/locale

  - 将原有内容全部注释，粘贴以下内容至locale配置文件中

        LANG="zh_CN.UTF-8"
        LANGUAGE="zh_CN:zh"
        LC_NUMERIC="zh_CN"
        LC_TIME="zh_CN"
        LC_MONETARY="zh_CN"
        LC_PAPER="zh_CN"
        LC_NAME="zh_CN"
        LC_ADDRESS="zh_CN"
        LC_TELEPHONE="zh_CN"
        LC_MEASUREMENT="zh_CN"
        LC_IDENTIFICATION="zh_CN"
        LC_ALL="zh_CN.UTF-8"

- 修改环境文件

      sudo nano /etc/environment

  在原内容后面新增以下内容

        LANG="zh_CN.UTF-8"
        LANGUAGE="zh_CN:zh"
        LC_NUMERIC="zh_CN"
        LC_TIME="zh_CN"
        LC_MONETARY="zh_CN"
        LC_PAPER="zh_CN"
        LC_NAME="zh_CN"
        LC_ADDRESS="zh_CN"
        LC_TELEPHONE="zh_CN"
        LC_MEASUREMENT="zh_CN"
        LC_IDENTIFICATION="zh_CN"
        LC_ALL="zh_CN.UTF-8"  

- 修改环境文件

      sudo nano /etc/profile  

  在原有内容下面新增 
    
      LANG="zh_CN.UTF-8"  

### 开机自动启动ssh命令

    sudo systemctl enable ssh
