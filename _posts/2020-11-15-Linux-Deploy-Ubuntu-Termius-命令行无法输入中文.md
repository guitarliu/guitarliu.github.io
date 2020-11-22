## Linux Deploy容器内安装Ubuntu后，Termius连接终端无法输入中文
需要安装中文语言包：
language-pack-zh-hans（简体中文）
language-pack-zh-hans-base
language-pack-zh-hant（繁体中文）
language-pack-zh-hant-base
~~~
sudo apt-get install language-pack-zh-han*

i~~~
## 修改配置文件locale
~~~
vim /etc/default/locale
~~~
将locale中初始内容注释，并添加以下内容：
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh:en_US:en"

最后:Sudo apt-get update，关闭Termius，重新打开即可显示和输入中 
