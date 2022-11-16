# klipper-on-android


**Run klipper, moonraker, fluidd, KlipperScreen on android system, one-click script for quick configuration.**


***Standing on the shoulders of giants!!!***

***grateful:***

***Original klipper, moonraker and xterm init scripts by @d4rk50ul1 (https://github.com/d4rk50ul1/klipper-on-android)***

***Original ttyACM0 initialization script by @CODERUS (https://gist.github.com/CODERUS/a5ec4a456f5b58186cbebb66a8542a2e)***

**Foreword:**

0. Although the steps in this tutorial are as comprehensive and detailed as possible, 
   it is not suitable for complete novice users because it involves basic linux system usage and klipper configuration.

1. The Android system in this tutorial must be rooted. Because the root method of each mobile phone hardware and system is different, 
   there are many tutorials on the Internet, so I won't repeat them here.
   
2. The software and hardware environment of this tutorial:

   Xiaomi 2S mobile phone
  
   16G ROM, 2G RAM

   Run MOKEE9.0 operating system based on android9.0

   The system has used MOKEE's official patch to obtain root privileges

   Brush and system root refer to the official tutorial:

   ROM download and flash: https://download.mokeedev.com/aries.html

   Get root permissions: https://bbs.mokeedev.com/t/topic/6577

3. In theory, this tutorial can be applied to any rooted Android phone, to be tested.

4. In theory, the debian system installed after installing the proroot container in termux can also be used, to be tested.

5. The printer control motherboard model: MKS SGEN-L V1.0, the klipper firmware has been burned in the SD card in the motherboard.


**Features of this tutorial:**

1. Use a separate APP to install the linux operating system under the graphical interface, configure the operating system to automatically restart, etc. Easy to manage and use.

2. klipper still uses the popular kiauh script to install, upgrade or uninstall. The KlipperScreen interface of the mobile phone or the web interface can be used to upgrade each module.

3. Use a one-click script to quickly configure the klipper family bucket, which is convenient and fast.

4. Based on my own experience, I modified and customized the basic configuration files of the klipper family bucket, and some key configurations are more practical.
           
5. After installation, no error is reported, and services such as klipper and moonraker can be individually controlled to start, restart, and close.

6. The user experience is basically the same as that of the Raspberry Pi, including input shaping and pressure compensation, mobile phone CPU temperature display, and online upgrade of printer motherboard firmware SD card.

################################################## ################################################## ###

***The installation process is long and the phone needs to be connected to the charger! ! ! ! ! !***

***This tutorial assumes:***

***Android phone is rooted! ! ! ! ! !***

***The klipper firmware has been flashed in the SD card in the motherboard: https://github.com/gaifeng8864/klipper-on-android/blob/main/klipper.bin***

***(The klipper firmware in SD card needs to be compiled according to the motherboard model, the firmware in this link is only for MKS SGEN-L V1.0)***

Required software:

mobile phone:

XServer-XSDL-1.20.51.apk (required) Download link: https://sourceforge.net/projects/libsdl-android/files/apk/XServer-XSDL/
    
linuxdeploy-2.6.0-259.apk (required) Download link: https://github.com/meefik/linuxdeploy/releases/download/2.6.0/linuxdeploy-2.6.0-259.apk

kerneladiutor_248.apk (open all CPU cores, recommended installation) Download link: https://f-droid.org/en/packages/com.nhellfire.kerneladiutor/

termux_118.apk (optional, install when needed) download link: https://github.com/termux/termux-app/releases/tag/v0.118.0

computer:

Xshell (required) official website address: https://www.netsarang.com/en/xshell/

Xftp (optional, recommended installation): https://www.netsarang.com/en/xftp/

## 0. Install XServer-XSDL ##

The installation of XServer-XSDL is relatively simple, just follow the system prompt and go directly to the next step.

Note: After the installation is complete, you need to click the "Change Device Settings" button at the top of the screen on the first startup interface to enter the setting interface, and then click "Mouse Simulation" --- "Mouse Simulation Mode" --- "Desktop version, no simulation" , then scroll down to the bottom and click Done. Otherwise the touch cannot be used.

If you miss the interface for the first startup, just close XServer-XSDL running in the background and start XServer-XSDL again.

## 1. Install kerneladiutor ##

Qualcomm processors have an MPD power consumption control scheme by default. By default, some CPU cores are turned off to control power consumption.
The biggest problem caused by this is that in the debian system, it will be found that the processor with 4 cores only recognizes 2 cores in most cases.
kerneladiutor is a simple and easy-to-use Android kernel management software, used to adjust the frequency and performance of CPU and GPU. All CPU cores can be forcibly turned on to make full use of the performance of the phone.

## 2. Install linuxdeploy ##

Install the apk file according to the system prompts. After the installation is complete, open the software and click on the upper left corner of the main interface "
![三横杠](https://user-images.githubusercontent.com/16047447/202127479-5174b558-7677-4cb6-8b69-dfbd6ef8e11b.png)"Open the software settings:

Lock screen (no)

Lock Wi-Fi (yes)

Wake lock (yes)

Autostart (yes)

Autostart delay (5) (set as needed, increase the number if you want to start later)

Track network changes (yes)

Other options remain default! ! ! ! ! ! ! ! ! !

! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! !


## 3. Install debian system ##

After setting, return to the main interface, click on the lower right corner "![滑动开关](https://user-images.githubusercontent.com/16047447/202127702-f66eca3e-0300-40f5-a1f0-43e42236b7fc.png)"Open the Linux system installation configuration.

Distribution (Debian)

Architecture (armhf) (Check your mobile phone processor model by yourself, if it supports 64 bits, choose arm64)

Distribution suite (stable)

Installation type (Directory)

Installation path (/data/debian11)

Username (print3D) (because it involves the path of the klipper configuration file, it is recommended to use this username)

User password: (123456) (set whatever you want, as long as you can remember it)

INIT (enable)

Init system (sysV)

SSH (enabled) (must be enabled, otherwise it will not be able to connect to the linux system)

GUI (enabled)

Graphics subsystem (X11)

Desktop environment (XTerm)

Other options remain default! ! ! ! ! ! ! ! ! !

! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! !


After the configuration is complete, return to the main interface

Click on the upper right corner "![三竖点](https://user-images.githubusercontent.com/16047447/202128541-77af60ad-6f61-4c7d-8e40-4b020f144e1f.png)
" Click "Install" (The installation process is relatively long, about 5-15 minutes depending on the network situation)

When "<<< deploy" appears at the bottom of the interface, the installation is complete

Click "STOP" at the bottom of the main interface, "<<< stop" will appear, and then click "START" (this step is necessary, otherwise the debian system will not start)

After the system is started, use Xshell to connect to the debian system (the IP address is displayed at the top of the main interface of the linuxdeploy software, the login name and password are set in the above steps, port 22, protocol ssh)

At this point, the debian system installation is complete! ! ! ! ! ! ! ! ! ! ! ! ! ! ! !

! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! !

## 4.klipper installation environment configuration ##

After logging in to the debian system with ssh, execute the following command:

   sudo usermod -a -G aid_inet,aid_net_raw root

###Because of the chroot container permission problem on the Android system, except for the initial login user, other users have no network permission by default, including the root user. This command can solve the problem that the root user cannot connect to the Internet when using the sudo command.

   sudo apt update

###Update system packages

   sudo apt install -y git vim wget

###Install the necessary tools and software

## 5. Install klipper using kiauh ##

   cd ~

### Enter the login user's home directory

   git clone https://github.com/th33xitus/kiauh.git

###Official kiauh script address

   git clone https://gitee.com/miroky/kiauh.git

###Domestic kiauh script address (choose one from the official address above)

   ./kiauh/kiauh.sh

###Start the script to start installing the klipper family bucket

### Need to install klipper, moonraker, fluidd (one-click script does not support Mainsail configuration), KlipperScreen these 4 components.
Every time a component is installed, it will prompt that the service cannot be started. This is the reason why the Android initialization system is not compatible with the klipper family bucket service startup method. Don’t worry about it. If it can be started, there is no need to configure it with a one-click script.
Component installation involves part of the compilation process, which takes a long time, so wait patiently. As long as each script can be automatically installed to the end, there is basically no problem.
