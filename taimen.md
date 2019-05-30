# Katsuna OS for the Pixel 2 XL

### Device important info

* **name**: Pixel 2 XL
* **board/device name**: taimen
* **arm architecture**: arm64

### Contents
1. [Set up the environment](#env)
2. [Before installing Katsuna OS for the first time](#first)    
    2.1. [Format Data partition](#format)
3. [Update to the correct stock Pixel image](#stock)
4. [Install a custom recovery partition (TWRP)](#recovery)      
    4.1. [Boot into TWRP Recovery](#recovery-boot)      
    4.2. [Install TWRP Recovery on the Pixel](#recovery-install)
5. [Install Katsuna OS](#install)       
    5.1. [Install the Katsuna OS ROM](#flash)   
    5.2. [Install Google Apps](#gapps)
6. [Update Katsuna OS](#update)     
    6.1. [Update to a normal Katsuna OS update](#normal-update)       
    6.2 [Update to a Katsuna Security Update](#security-update)


<a name="env"></a>
## 1. Set up the working environment (for Windows)

Installing Katsuna OS is a unofficial modification to your device. Every time you want to install, update and/or factory reset it, make sure you have your working environment ready. You are going to need:

##### 1.1. **Open CMD.exe** (Command Prompt)
by searching for it in Windows Start.

##### 1.2. **Download Android SDK Tools**     
> Go [here](https://developer.android.com/studio/index.html#download) to download the Android SDK, which will give you most updated version of adb and fastboot. Scroll to the bottom of the page and find Other Download Options>SDK Tools Only, and grab the right version for your OS. While it's downloading create a folder in C:\ called SDK (C:\SDK). Once you've downloaded the zip you can extract it into your C:\SDK folder. Navigate to C:\SDK\android-sdk-windows and open SDK Manager.exe. In SDK Manager you need to install the following packages:

* Tools - Android SDK Tools, Android SDK Platform-tools
* Extras - Android Support Library, Google USB Driver     

##### 1.3. **Enable Developer Settings** in Android OS        
> Go into Settings/About Phone, scroll down and click on “build number” continuously until you see a toast notification telling you that you've enabled Developer Options. Go back to your Settings menu and enter Developer Options, scroll down and click on the **Enable OEM Unlock** (or "Enable OEM Unlocking") checkbox, also make sure you enable **USB Debugging** while you're in the Developer Options menu. Unplug and re-plug your device until the "ADB accept key" dialog is shown.

##### 1.4. **Test your adb/fastboot commands**          
Type these commands in the CMD window:
```
cd C:\SDK\platform-tools
adb devices
```
It should return your device **serial** number, if so, adb is working.

Next, power off your device. Turn it on again by pressing **(power + volume down)** and type this command in the CMD window.
```
fastboot devices
```
It should return your device **serial** number, if so, fastboot is working.

##### 1.5. **An Unlocked Bootloader**      
The bootloader screen will show you if the device's bootloader is unlocked. If it isn't, you will need to unlock it by typing this command:

**This will erase all user data from the device!**
```
fastboot flashing unlock_critical
```
It will ask you for confirmation using the volume buttons and the power menu at this point, do it.

<a name="first"></a>
## 2. Before installing Katsuna OS for the first time

If you are here, this is your first time installing Katsuna OS! After [setting up the working environment as described in the previous step](#env), you will also need to do the following **BEFORE** installing Katsuna OS:

2.1. Format Data partition     
2.2. Install a custom recovery partition (TWRP)     
2.3. **DO NOT** reboot to Android OS after any step     

<a name="format"></a>
#### 2.1. Format Data partition
Power off your device. Turn it on again by pressing **(power + volume down)** and type this command in the CMD window:

  **Please note: this will erase all user data from the device!**       
```
fastboot format userdata
```

<a name="stock"></a>
## 3. Update to the correct stock Pixel image

Katsuna OS is based on the official version of Android 8.1 (July security update: OPM2.171026.006.H1). To ensure the best compatibility with Katsuna OS for your device, you will need to install the bootloader, radio, and the vendor partition of this version.

##### 3.1. Download the [OPM2.171026.006.H1 stock pixel image for Pixel 2 XL](https://dl.google.com/dl/android/aosp/taimen-opm2.171026.006.h1-factory-57328312.zip)
after reading and agreeing with Google's [Terms & Conditions](https://developers.google.com/android/images#legal)
##### 3.2. Extract the zip file
Find the **bootloader-taimen-tmz12g.img**, **radio-taimen-g8998-00202-1802061358.img** and **image-taimen-opm2.171026.006.h1.zip** files.     
Extract the **image-taimen-opm2.171026.006.h1.zip** and find the **vendor.img** file.
##### 3.4. Copy all the above mentioned files inside:
```
C:\SDK\platform-tools\
```
##### 3.5. Power off your device. Turn it on again by pressing **(power + volume down)** and type these commands in the CMD window:
```
fastboot flash bootloader bootloader-bullhead-bhz11e.img   
fastboot flash radio radio-bullhead-m8994f-2.6.33.2.14.img   
fastboot flash vendor vendor.img
```

<a name="recovery"></a>
#### 4. Install a custom recovery partition (TWRP)
The recovery partition in your device is used to apply software updates to the device, e.g. OTA updates, and to erase user data and cache, e.g. for troubleshooting or preparing the device for resale (factory reset). For installing Katsuna OS, you are going to need to install a popular alternative, TWRP Recovery.

1. Download [TWRP Recovery 3.3.0-0](https://dl.twrp.me/taimen/)
2. Download [TWRP Pixel2 Installer 3.3.0-0](https://dl.twrp.me/taimen/twrp-pixel2-installer-taimen-3.3.0-0.zip)
3. Copy the downloaded files inside:
```
C:\SDK\platform-tools\
```
<a name="recovery-boot"></a>
##### 4.1. Boot into TWRP Recovery
You can do that by powering off your device. Turn it on again by pressing **(power + volume down)** and type these commands in the CMD window:
```
fastboot boot twrp-3.3.0-0-taimen.img
```

**BE CAREFUL!** From now on and before installing the Pixel2 Installer, don't reboot into the stock Android at any part of the process, or the custom TWRP will be overwritten by the stock recovery and you will have to start over!

<a name="recovery-install"></a>
##### 4.2. Install TWRP Recovery on the Pixel
1. Push the TWRP Pixel2 Installer file to the device by typing this command in the CMD window:        
```
adb push twrp-pixel2-installer-taimen-3.3.0-0.zip /sdcard/
```     
2. Install the TWRP Pixel2 Installer file     
```
* Select the install option from the TWRP home screen.
* Select the TWRP Pixel2 Installer zip
* Swipe to install
```     

<a name="install"></a>
## 5. Install Katsuna OS

Every time you want to install Katsuna OS:

* Make sure you have [already updated to the correct stock pixel image](#stock).
* [Install](#flash).

<a name="flash"></a>
### 5.1. Install the Katsuna OS ROM file

1. Download the ROM from [here](http://updater.katsuna.com/files/taimen/latest).
2. [Boot into TWRP Recovery](#recovery-boot)
3. Perform a full wipe in TWRP      
```
* Select the wipe option from the TWRP home screen.
* Select advanced wipe.
* Check the system, data, and dalvik/art cache options.
* Swipe to wipe.
```          
4. Copy the downloaded ROM file inside:     
```
C:\SDK\platform-tools\
```     
5. Push the ROM file to the device by typing this command in the CMD window (replace FILENAME with the name of the downloaded file):        
```
adb push FILENAME.zip /sdcard/
```     
6. Install the ROM file     
```
* Select the install option from the TWRP home screen.
* Select the ROM zip
* Swipe to install
```
7. [Install TWRP Recovery on the Pixel](#recovery-install)   
8. Don't reboot yet, don't press "reboot system". Instead:
```
* Select the reboot option from the TWRP home screen.
* Select recovery
```       
The device should reboot into TWRP recovery again.      
8. (Optional): [Install Google Apps](#gapps). Make sure you only try to install it after you have rebooted **once** since the ROM installation!        
9. Select "Reboot System" and wait for Katsuna OS to load for the first time.

<a name="gapps"></a>
### 5.2. Install Google Apps (Optional)
*Open-GApps is an independent third party GApps (Google Apps) distribution service that Katsuna has no affiliation with. Use at your own discretion.*

You can use the Google Play Store and Google Apps with your Katsuna OS installation with an extra step. During [installation](#flash):

1. Download [Nano Open-GApps package](http://opengapps.org/) **for Android 8.1 & arm64**    
2. Copy the downloaded file inside:
```
C:\SDK\platform-tools\
```
3. Push the file to the device by typing this command in the CMD window (replace FILENAME with the name of the downloaded file):
```
adb push FILENAME.zip /sdcard/
```
4. Install the Google Apps file
```
* Select the install option from the TWRP home screen.
* Select the GApps zip
* Swipe to install
```

<a name="update"></a>
## 6. Update Katsuna OS

Katsuna OS can be updated:

* Manually, by using the [installing procedure](#install).        
If you choose this method, there are no extra steps.

* Through the Updater App inside Katsuna OS.        
If you update the ROM through the Updater app:

<a name="normal-update"></a>
##### 6.1. Update to a new normal Katsuna OS update
The Updater app will let you know automatically if a new update has been found, and you will be able to download the update and apply it with a few taps with no PC involved, utilising the double partition system of the Pixel. After the installation is finished, you'll be able to boot into the new system with a simple restart.

<a name="security-update"></a>
##### 6.2. Update to a new Katsuna Security Update
After a new Katsuna [Security update](https://source.android.com/security/bulletin/), you will need to [download the relevant stock pixel image and install ONLY the vendor.img file again](#stock).
