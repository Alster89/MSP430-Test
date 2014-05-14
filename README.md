# MSP430 Test #
---
## Introduction ##
This repository is a testbed for code that is to be used with Texas Instruments' [MSP430 Launchpad](http://www.ti.com/tool/msp-exp430g2). This project is a work in progress and may be abandoned soon (depending on which direction my research takes me)

## Installation and Setup##
Since I develop on a Mac, here's what I did to get everything working properly. Thanks to the [Media Computing Group](http://hci.rwth-aachen.de/msp430) for the excellent tutorial. 

1. Install Xcode and Xcode command line tools
2. Install Macports
3. Using Macports, install ```msp430-gcc```, ```msp430-libc```, ```mspdebug```.
4. ```mspdebug``` does not play nice with the OSX HID drivers. As a result, one needs to install a kernel extension (kext). Follow the following steps to do so under OS X Mavericks and Xcode 5.1.
	1. Download the kext from [Colossal Dynamic's Github](https://github.com/colossaldynamics/ez430rf2500).
	2. Open the project in Xcode
	3. Double click the little yellow warning triangle in Xcode so that the recommended changes page pops up. Allow Xcode to make the recommended changes. This includes changing the compiler to the most recent version.
	4. Build the project.
	5. In the Xcode sidebar, in the ```projects``` folder, there should be a file called ```ez430rf2500.kext```. Right click, show in finder, and drag the .kext file to your desktop.
	6. Open the terminal and run the following commands. You will need to use ```sudo``` for most commands. After running the commands, reboot your computer. ```mspdebug``` should now be ready to use.

```
cd /System/Library/Extensions
cp -R ~/Desktop/ez430rf2500.kext .
chown -R root:wheel ez430rf2500.kext
chmod -R 755 ez430rf2500.kext
```

## Compiling & Uploading ##
All code can be compiled by running ```make``` in the working directory. The makefile has been designed so that all files inside the working directory will be automatically compiled. However, any ```*.c``` files that live in external folders will need to be added to the ```EXTERN_FILES``` line, all separated by spaces. To summarize, the following steps will need to be completed to modify the makefile for other projects:

1. Change the filename on line 28.
2. Change the device name on line 29.
3. Add any external ```*.c``` files to line 30, separated by spaces.

Programs can be uploaded by running ```make upload```. It should not be necessary to compile before running ```make upload```. Cleaning can be done with ```make clean```.

# Project Descriptions #
* **Blink** - Blinks the LEDs on and off