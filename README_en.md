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
  
   16G body storage, 2G running memory

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

cell phone:

XServer-XSDL-1.20.51.apk (required) Download link: https://sourceforge.net/projects/libsdl-android/files/apk/XServer-XSDL/
    
linuxdeploy-2.6.0-259.apk (required) Download link: https://github.com/meefik/linuxdeploy/releases/download/2.6.0/linuxdeploy-2.6.0-259.apk

kerneladiutor_248.apk (open all CPU cores, recommended installation) Download link: https://f-droid.org/en/packages/com.nhellfire.kerneladiutor/

termux_118.apk (optional, install when needed) download link: https://github.com/termux/termux-app/releases/tag/v0.118.0

computer:

Xshell (required) official website address: https://www.netsarang.com/en/xshell/

Xftp (optional, recommended installation): https://www.netsarang.com/en/xftp/


