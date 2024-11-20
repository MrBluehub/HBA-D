HBA-D - High-Band Antenna Diagnostics
==========================================================
Lofar tile tester based on Erik Kaashoek's TinySA ultra:
https://github.com/erikkaashoek/tinySA
https://www.tinysa.org

[![GitHub release](http://img.shields.io/github/release/erikkaashoek/tinySA.svg?style=flat)][release]
[![CircleCI](https://circleci.com/gh/erikkaashoek/tinySA.svg?style=shield)](https://circleci.com/gh/erikkaashoek/tinySA)

[release]: https://github.com/erikkaashoek/tinySA/releases

<div align="center">
<img src="/doc/tinySA.jpg" width="480px">
</div>

# About

HBA-D aims to bring field diagnostics of HBA Tiles in a portable device utilizing a custom io bord added to the TinySA. This small handheld Spectrum Analyzer (SA) functions as the user interface

This repository contains source of HBA-D firmware, largely based on the TinySA.


### Update HBA-D Firmware:

# prerequisites: 



    Linux PC to compile firmware with the below dependencies 

    Install GIT : sudo apt-get install git  
    (with sudo you elevate the terminal with administrative privileges required to install software using ‘apt get’, which is a application that allows rapid download and installation of software build into linux. Using apt-get we install git to easily clone the latest HBA-D from its git repositor.) 

    Install Make: sudo apt install make  
    (installs the ‘make’ library to linux, in this case it is used to compile software from .c to .bin files) 

    Windows PC with STM32 Cube Programmer 

### Linux (ubuntu) 

Download arm cross tools from [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads).

    $ wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2018q4/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2
    $ sudo tar xfj gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 -C /usr/local
    $ PATH=/usr/local/gcc-arm-none-eabi-8-2018-q4-major/bin:$PATH
    $ sudo apt install -y dfu-util

## Fetch source code

Fetch source and submodule.

    $ git clone https://github.com/MrBluehub/HBA-D.git
    $ cd HBA-D
    $ git submodule update --init --recursive

## Build

Just make in the directory.

    $ make TARGET="F303"

    (Remove TARGET="F303" for non-ultra, custom software is untested on this device.) 


## Flash firmware

First, make device enter DFU mode by one of following methods.

* Jumper BOOT0 pin at powering device by holding down the rocker button
* Select menu Config->DFU (needs recent firmware)

Then, flash firmware using dfu-util via USB.

    $ dfu-util -d 0483:df11 -a 0 -s 0x08000000:leave -D build/ch.bin

Or simply use make.

    $ make flash

## Flashing using a windows pc

Move the file tinySA4.bin from /usr/local/HBA-D/build/ to the windows pc. This is the firmware compiled using the Linux pc required for updating. Currently there is no known way to compile the software using a windows tool.

Launch STM32 Cube Programmer 

### Video instructions: 

https://www.youtube.com/watch?v=i8CYCua8vqQ&t=396s 

TLDR: Put TinySA in boot mode by holding down the menu button while turning on the device. Make a USB connection to a Windows pc and launch STM32 CubeProgrammer 

### Written instructions:

Select USB as the desired connection method, refresh and select the HBA-D (likely USB1).

Select "open file" and choose the firmware you compiled in previous steps (tinySA4.bin)

Click the download button to start the update process.

After the completion screen you can Disconnect in CubeProgrammer, disconnect the TinySA and reboot into your new firmware. 

## TinySA specific information below:

### Documentation

* [tinySA User Guide](https://tinySA.org/wiki/)

### Reference

* [Specification](https://tinysa.org/wiki/pmwiki.php?n=Main.Specification)
* [Technical info](https://tinysa.org/wiki/pmwiki.php?n=Main.TechnicalDescription)

### Note

tinySA is a trademark owned by its respective owner. Unauthorized use of the name tinySA not permitted

### Authorized Distributor

* [See the Wiki](https://tinysa.org/wiki/pmwiki.php?n=Main.Buying)

### Credit

* [@erikkaashoek](https://github.com/erikkaashoek)

### Contributors

* [@edy555](https://github.com/edy555)
* [@hugen79](https://github.com/hugen79)
* [@cho45](https://github.com/cho45)
* [@DiSlord](https://github.com/DiSlord/)
