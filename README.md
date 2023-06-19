# klipper-on-android

**在android系统上运行klipper，moonraker，fluidd，KlipperScreen，一键脚本快速配置。**

**Run klipper, moonraker, fluidd, KlipperScreen on android system, one-click script for quick configuration.**

**The English version of the tutorial is here: [README_en.md](https://github.com/gaifeng8864/klipper-on-android/blob/main/README_en.md)**


**视频教程在这里：**

B站：

[【保姆级教程】告别树莓派，安卓klipper全新安装方案+一键配置脚本，只需一点，从此告别安卓手机只能换脸盆的命运](https://www.bilibili.com/video/BV1BG4y1t7RR/?vd_source=7fb5d23ecaaec9c060d89fdde67b3d1b)

YOUTUBE：

[【教程】告别树莓派，安卓klipper全新安装方案+一键配置脚本](https://youtu.be/s1tdqg6ke4w)




***站在巨人的肩膀上！！！***


***感谢:***

***klipper, moonraker 和 xterm 初始化脚本来自 @d4rk50ul1***

***(https://github.com/d4rk50ul1/klipper-on-android)***

***ttyACM0 初始化脚本来自 @CODERUS***

***(https://gist.github.com/CODERUS/a5ec4a456f5b58186cbebb66a8542a2e)***




**前言：**

**特别说明：**
本教程里的安装方案使用的安卓系统最好选择安卓5到安卓9之间的版本。低于安卓5系统需要使用低版本linuxdeploy，高于安卓9系统可能会有权限相关的兼容性问题。另外，如果遇到openssh自动启动失败（表现为无法使用ssh连接debian系统），这种情况一般是安卓内核与linuxdeploy兼容问题，需要更换不同内核版本的安卓系统（注意，是不同内核版本）。

0.本教程虽尽量做到步骤全面和详细，但是因为涉及基本的linux系统使用和klipper配置，所以并不适合完全小白用户。不过，都已经准备使用安卓手机运行klipper了，相信这些已经不是问题。

1.本教程中安卓系统必须root。因每种手机硬件和系统的root方法各有不同，网络上教程很多，这里不再赘述。

2.本教程软硬件环境：

  小米2S手机
  
  16G机身存储，2G运行内存
		
  运行基于android9的魔趣9.0操作系统
		
  系统已使用魔趣官方补丁获取root权限
		
  刷机及系统root参考官方教程：
		
  ROM下载与刷机：https://download.mokeedev.com/aries.html
		
  获取root权限：https://bbs.mokeedev.com/t/topic/6577
		
3.理论上，只要能root的安卓手机此教程都能适用，待测试。	
	  
4.理论上，在termux里安装proot容器后安装的debian系统也可以使用，待测试。

5.打印机控制主板型号：MKS SGEN-L V1.0 ，主板内SD卡中已烧录klipper固件。
	  
	  
**本教程特点:**

1.使用一个单独的APP在图形界面下安装linux系统，配置系统自动重启，系统中文汉化等。方便管理和使用。

2.klipper系统依旧使用流行的kiauh脚本进行安装，升级或卸载。手机KlipperScreen界面或者网页界面都可以进行升级操作。

3.使用一键脚本对klipper全家桶进行快速配置，方便快捷。
			
4.结合我自己的使用经验，修改定制了klipper全家桶的基本配置文件，一些关键配置更加实用。
           								
5.安装好以后无任何报错，可单独控制klipper，moonraker等服务启动，重启，关闭。
			
6.使用体验与树莓派基本没有区别，包括使用输入整形与压力补偿，手机CPU温度显示，打印机主板固件SD卡在线升级等。
			
#######################################################################################################			  


***安装过程较长，手机需要连接到充电器！！！！！！***

***本教程假设：***

***安卓手机已root ！！！！！！***

***主板内SD卡中已烧录klipper固件：[klipper(MKS SGEN-L V1.0).bin](https://github.com/gaifeng8864/klipper-on-android/blob/main/klipper(MKS%20SGEN-L%20V1.0).bin?raw=true)***

***（SD卡中的klipper固件需要根据主板型号进行编译，此链接中的固件只适用于MKS SGEN-L V1.0）***


需要用的软件：

手机端：

XServer-XSDL-1.20.51.apk（必装） 下载链接：https://sourceforge.net/projects/libsdl-android/files/apk/XServer-XSDL/
    
linuxdeploy-2.6.0-259.apk（必装） 下载链接：https://github.com/meefik/linuxdeploy/releases/download/2.6.0/linuxdeploy-2.6.0-259.apk

kerneladiutor_248.apk（开启所有CPU核心，推荐安装） 下载链接：https://f-droid.org/en/packages/com.nhellfire.kerneladiutor/

termux_118.apk（选装，需要时再安装）下载链接：https://github.com/termux/termux-app/releases/tag/v0.118.0
		
电脑端：

Xshell（必装）官网地址：https://www.netsarang.com/en/xshell/

Xftp（选装，建议安装）：https://www.netsarang.com/en/xftp/




## 0.安装XServer-XSDL ##

XServer-XSDL安装比较简单，按系统提示直接下一步就可以了。

注意：安装完成后需要在第一次启动的界面点击屏幕上方 “更改设备设置” 按钮进入设置界面，依次点击 “鼠标模拟”---“鼠标仿真模式”---“桌面版，无仿真”，然后下拉到最底下点击“完成”。否则触摸无法使用。

如果错过了第一次启动的界面，关闭XServer-XSDL后台运行后再次启动XServer-XSDL即可。

## 1.安装kerneladiutor ##

高通处理器默认有个MPD功耗控制方案，默认情况下会关闭部分CPU核心来控制功耗。
由此带来的最大的问题就是在debian系统里会发现4核心的处理器大多数情况下却只识别出2个核心。
kerneladiutor是简单好用的安卓系统的内核管理软件，用来调整CPU和GPU的频率和性能。可以强制开启所有CPU核心，充分利用手机的性能。

## 2.安装linuxdeploy ##

根据系统提示安装apk文件，安装完成后打开软件点击主界面左上角“![三横杠](https://user-images.githubusercontent.com/16047447/201450191-fc8d09bc-7ae5-4e9a-97a2-a92c5fdf36c2.PNG)
”打开软件设置：

	屏幕常亮  （勾选）
	
	锁定Wi-Fi （勾选）

	CPU唤醒   （勾选）

	开机自启动 （勾选）

	语言      （简体中文）

	启动延迟   （5）  （以秒为单位，根据需要设置，想迟一点启动就将数字调大）

	联网更新   （勾选）

其他选项保持默认！！！！！！！！！！

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！


## 3.安装debian系统 ##

设置好后回到主界面，点击右下角“![滑动开关](https://user-images.githubusercontent.com/16047447/201450293-096d3977-1b77-435d-8106-bf95c27d6052.PNG)
”打开linux系统安装配置。

	发行版 （Debian）

	架构（armhf）（自行查询自己手机处理器型号，如果支持64位就选arm64）

	发行版本 （stable）

	源地址 （ http://ftp.cn.debian.org/debian/ ）（国内源安装更快）

	安装类型 （目录）

	安装路径 （/data/debian11）

	用户名 （print3D）（因为涉及到klipper配置文件的路径，所以建议就用这个用户名）

	密码：（123456）（随便设置，能记住就行）

	本地化 （zh-CN.UTF-8）（系统汉化，便于使用）

	初始化 （启用）

	初始化系统 （sysV）

	挂载点 （可选，此应用场景下一般用不到）

	挂载点列表 （/sdcard/-/mnt/sdcard/）（可选，此应用场景下一般用不到）

	SSH （启用）（必须开启，否则连不上linux系统）

	图形界面 （启用）

	图形子系统 （X11）

	图形界面设置 （取消勾选自动打开XServer-XSDL）（一键配置脚本里已经配置自动开启XServer-XSDL客户端，此处不需要勾选）

	桌面环境 （XTerm）

其他选项保持默认！！！！！！！！！！

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

配置完成后回到主界面

点击右上角“![三竖点](https://user-images.githubusercontent.com/16047447/201450321-113c378f-88ec-4009-871f-0c76eabf3004.PNG)
” 点击 “安装” （安装过程比较漫长，根据网络情况大概在5-15分钟）

界面下方出现 "<<< deploy" 时说明安装完成

点击主界面下方“停止”，出现"<<< stop" 再点击“启动”（这一步不能少，否则debian系统启动不了）

系统启动完成后使用Xshell连接debian系统（IP地址显示在linuxdeploy软件主界面最上方，登录名和密码就是上面步骤里设置的，端口22，协议ssh）

至此，debian系统安装完成！！！！！！！！！！！！！！！！

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！


## 4.klipper安装环境配置 ##

ssh登录进入debian系统后执行以下命令：

	sudo usermod -a -G aid_inet,aid_net_raw root

###由于安卓系统上chroot容器权限问题，除初始登录用户外，默认其他用户没有网络权限，包括root用户。此命令可以解决使用sudo命令时root用户无法联网的问题。

	sudo apt update

###更新系统软件包

	sudo apt install -y git vim wget

###安装必要的工具软件

## 5.使用kiauh安装klipper ##

	cd ~

###进入登录用户家目录

	git clone https://github.com/th33xitus/kiauh.git

###官方kiauh脚本地址

	git clone https://gitee.com/miroky/kiauh.git

###国内kiauh脚本地址（与上面官方地址二选一即可）

	./kiauh/kiauh.sh
	
###启动脚本开始安装klipper全家桶

###需要安装klipper，moonraker，fluidd（一键脚本暂时不支持Mainsail配置），KlipperScreen 这4个组件。
每安装完一个组件都会提示无法启动服务，这是安卓初始化系统与klipper全家桶服务启动方式不兼容的原因，不用管它，如果能启动起来就不用一键脚本去配置了。
组件安装涉及部分编译过程，耗时较长，耐心等待。只要是每个脚本都能自动安装到最后，基本就没有问题。

## 6.klipper全家桶配置 ##

使用Xftp或命令行进入以下路径：

	/home/print3D/printer_data/config/

将里面的 fluidd.cfg,moonraker.conf,printer.cfg 进行备份之后把原文件删除。

	cd ~

###进入登录用户家目录

将本仓库里的fluidd.cfg,homing_override.cfg,moonraker.conf,printer.cfg 这4个文件下载后放到 /home/print3D/printer_data/config/ 路径下。

或者想省事，直接执行以下命令：

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/fluidd.cfg

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/homing_override.cfg

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/moonraker.conf

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/printer.cfg

***注意：*** printer.cfg 这个配置文件需要根据自己的打印机控制主板型号进行参数更改。具体请参考各主板配置说明。


***！！！！！！将打印机主板上电启动，使用OTG线将手机和打印机主板连接！！！！！！***

回到debian系统内执行如下命令：

 	cd ~

###进入登录用户家目录

	sudo wget https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/configuration_klipper_family.sh

	bash configuration_klipper_family.sh

执行完毕后重启手机，没有问题的话klipper全家桶和XServer-XSDL会自动启动并连接到打印机，屏幕上会显示KlipperScreen经典界面。


***注意：*** 如果手机硬件已正确连接到打印机控制主板，但是运行脚本时依旧提示 " **Please connect your phone to the printer** "。
     debian系统内执行以下命令查看设备识别状态：

     ls -al /dev/

使用识别的设备名称执行： 

	bash configuration_klipper_family.sh -p "识别的设备名称"


祝大家每一次3D打印都能成功！！！



**备注：**

**构建和刷写SD卡固件请参考：https://www.klipper3d.org/Installation.html**

**SD卡固件在线更新请参考：https://www.klipper3d.org/SDCard_Updates.html**




