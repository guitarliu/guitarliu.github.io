---
layout: post
title: "ESP8266-NodeMCU-Lua-V3 MicroPython固件烧写及与1.44''-ST7735-128x128-TFT屏连接"
date: 2021-12-31
excerpt: "ESP8266-NodeMCU-Lua-V3 MicroPython firmware programming and connects with 1.44''-ST7735-128x128-TFT Screen"
tags: [MicroPython, ESP8266-NodeMCU-Lua-V3, Firmware Programming, ST7735, Connect TFT]
comments: true
---

<center>

![](https://pixabay.com/get/gb9f29b22639acb2aa3bcd160d948fae4cc2ee50b11bc0d0d6c44cb1547790c171825cf3b13a1ba34dd03cd4493224b7db26b65fa66577b73dc00b9a102fa52cba2b904f9d0226634db8c12cd1172a283_1280.jpg)<br><br>

</center>


##### 材料清单

<font color=darkblue size=1>

|名称|型号|尺寸|
|:----:|:----:|:----:|
|ESP8266|NodeMCU Lua V3|-|
|TFT屏|MAR1441|1.44"|

</font>

##### Micropython固件的刷入

&ensp;&ensp;&ensp;<font size=1>访问[MicroPython](https://micropython.org/download/) 官方网站，点击MCU版本为esp8266的链接，选择相应flash闪存的版本，最后下载对应固件；下载完成后刷入固件，具体方法见[官方文档説明](http://docs.micropython.org/en/latest/esp8266/tutorial/intro.html#deploying-the-firmware)。</font>

<font size=1>

&ensp;&ensp;&ensp;下载命令行烧写工具（桌面版烧录工具 ESP8266 DownloadTool请参考其他教程）

```Python
pip install esptool
```

&ensp;&ensp;&ensp;将ESP8266通过USB数据线连接电脑，进入电脑设备管理器，点击“端口”，找到ESP8266所在端口(一般为COM3或COM4)。<br>
&ensp;&ensp;&ensp;转到固件下载后位置，右键“在Windows终端中打开”，进入固件所在文件夹目录，通过如下命令依次完成原有flash闪存擦除及MicroPython固件的刷入。

```Python
esptool.py --port COM4 erase_flash

esptool.py --port COM4 --baud 115200 write_flash --flash_size=detect  0 esp8266-20210902-v1.17.bin
```
***注意：COM4需要改为开发板连接电脑后的实际端口号***
</font>

##### 利用Putty通过串口连接开发板

<font size=1>&ensp;&ensp;&ensp;打开Putty，选择Serial，Serial line填入开发板端口号，Speed=115200；点击Putty——Category界面左下角的Serial选项；
- Serial line to connect to: 端口号
- Speed(baud): 115200
- Data bits: 默认为8
- Stop bits: 默认为1
- Parity: None
- Flow control: None

&ensp;&ensp;&ensp;设置完成后，点击右下角“Open”，进入MicroPython命令行。</font>

##### ESP8266连接无线网

<font size=1>

```Python

import network

wlan = network.WLAN(network.STA_IF) # create station interface

wlan.active(True)       # activate the interface

wlan.scan()             # scan for access points

wlan.isconnected()      # check if the station is connected to an AP

wlan.connect('essid', 'password') # connect to an AP

wlan.config('mac')      # get the interface's MAC address

wlan.ifconfig()         # get the interface's IP/netmask/gw/DNS addresses
```
***详细代码参照 [ESP8266快速指引](http://docs.micropython.org/en/latest/esp8266/quickref.html)。***
</font>

##### ESP8266配置webrepl客户端并连接
<font size=1>

```Python
import webrepl_setup
```
&ensp;&ensp;&ensp;按照提示，输入密码并选择开机自启。打开 https://micropython.org/webrepl 并将ESP8266 IP地址修改为试验机IP，点击connect，输入密码后进入micropython命令行，即可上传和下载脚本文件。
</font>

##### st7735——TFT屏与ESP8266连接方式
<font size=1>

|TFT屏|连接|ESP8266|对应ESP8266引脚|对应引脚值|
|:----:|:----:|:----:|:----:|:----:|
|_VCC_ (电源正)|$\longrightarrow$|3V|-|-|
|_GND_ (电源地)|$\longrightarrow$|G|-|-|
|_GND_|$\longrightarrow$|-|-|-|
|_NC_(无定义)|$\longrightarrow$|-|-|-|
|_NC_(无定义)|$\longrightarrow$|-|-|-|
|_LED_(背光控制输入)|$\longrightarrow$|3V|-|-|
|_CLK_(SPI时钟输入)|$\longrightarrow$|D5|GPIO14|14|
|_SDI_(SPI数据输入)|$\longrightarrow$|D7|GPIO13|13|
|_RS_|$\longrightarrow$|D4|GPIO2|2|
|_RST_(屏的复位)|$\longrightarrow$|D2|GPIO4|4|
|_CS_(SPI片选输入)|$\longrightarrow$|D8|GPIO15|15|

</font>

##### st7735——TFT屏 MicroPython驱动模块
<font size=1>&ensp;&ensp;&ensp;st7735 TFT屏的驱动模块为MicroPython编写，具体参考: [st7735-esp8266-micropython](https://github.com/cheungbx/st7735-esp8266-micropython)。
将驱动脚本文件通过webrepl客户端上传至开发板，随后才可实现导入模块并调用相关函数。

```Python
from st7735 import TFT, TFTColor
from sysfont import sysfont
from machine import SPI,Pin

#hardware SPI, HSPI
dc=2
rst=4
cs=15
spi = SPI(1, baudrate=8000000, polarity=0, phase=0)

tft=TFT(spi,dc,rst,cs)
tft.init_7735(tft.GREENTAB128x128)
tft.rotation(3)
tft.fill(TFT.BLACK)
```
***注意: dc=2,rst=4,cs=15是通过连接ESP8266的引脚值得出，且为st7735模块所需参数，具体代码详[st7735-esp8266-micropython](https://github.com/cheungbx/st7735-esp8266-micropython)文档。***

</font>

##### st7735——TFT屏 MicroPython显示图片
<font size=1>&ensp;&ensp;&ensp;[st7735-esp8266-micropython](https://github.com/cheungbx/st7735-esp8266-micropython)源代码已给出相应参考代码，支持的图片格式为BMP，其他格式需要先转换BMP格式；对于128x128屏来説，修改后的BMP图片尺寸不宜超过128x160，但也勿将BMP图片尺寸保持为128x128(经试验，该尺寸无法显示)，最佳BMP图片尺寸为128x120~128x130；
</font>

##### 最终成果
<font size=1>
&ensp;&ensp;&ensp;若要 ESP8266 开机通电即可运行某程序，需将程序保存在 main.py 中并通过webrepl上传到开发板，重启后即可实现自启动运行。<br>
&ensp;&ensp;&ensp;关注公众号“Guitarliu”，并回复“st7735屏驱动”获取main.py文件。
</font>
