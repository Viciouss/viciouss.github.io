---
layout: post
title: Building the kernel
date: 2021-07-17 18:30:00 +0200
---

## The sobering

With the serial connection working, I could get my hands dirty building kernels, right? Well there, not so fast. Where to actually start on a 5.2 kernel? Aside from all the vendor changes and Android kernel patches, there have been 43 major updates in between the Samsung kernel and mainline with lots of internal API changes.Knowing only the old vendor kernel and how it is booted with a <a href="https://github.com/Viciouss/android_kernel_samsung_smdk4412/blob/cm-14.1/arch/arm/mach-exynos/mach-p4notepq.c" target="_new">board file</a>, I had to learn what a <a href="https://www.kernel.org/doc/html/latest/devicetree/usage-model.html">device tree</a> is. Very disappointing at first, as there was this big hurdle before even being able to build the kernel, but after a while it clicked and as it turned out, I could very much benefit from this right in the next step.

## Device Trees

Both the board file and the device tree describe the hardware of the device. The board file is explicit in this regard as it is written in C code and it loads the drivers directly, it's rather inflexible and if you want to share code with similar devices, it can get messy quickly. The "modern" approach for ARM devices is a  device tree. It's a language and data structure on its own, it is abstract and can be split up in smaller parts. You have a common SoC for a dozen devices? Just include the SoC device tree in your board tree and add the additional drivers on top, you are good to go. The abstract nature of device tree files also enables them to be used in other places than the kernel, e.g. a bootloader like U-Boot.

For the linux kernel, device tree files are compiled into device tree binaries (dtb files) which can then be read on boot to set up the system accordingly. I could gather a lot of information from the existing Exynos4 <a href="https://github.com/torvalds/linux/blob/v5.2/arch/arm/boot/dts/exynos4412-midas.dtsi" target="_new">dts files</a> which powered <a href="https://github.com/torvalds/linux/blob/v5.2/arch/arm/boot/dts/exynos4412-i9300.dts" target="_new">some</a> <a href="https://github.com/torvalds/linux/blob/v5.2/arch/arm/boot/dts/exynos4412-i9305.dts" target="_new">Samsung</a> <a href="https://github.com/torvalds/linux/blob/v5.2/arch/arm/boot/dts/exynos4412-n710x.dts" target="_new">devices</a> in mainline at that time. I added a new device tree, included the Exynos4412 one and looked for matching nodes in the midas tree, changed IRQ and GPIO configurations and then added some other nodes like the max17042 battery monitor for example. With this minimal tree in place, only the defconfig was missing to create an initial kernel image.

## defconfig and building the kernel

A defconfig file describes which architecture code and drivers get compiled in the kernel image. The exynos_defconfig looked promising, it already contains all the Exynos4 base drivers and some more, so I added the missing drivers and build the kernel:

```shell
# we want to compile for a different architecture, the kernel build needs to know this
export ARCH=arm
# a cross compiler toolchain is needed to do this of course
export CROSS_COMPILE=/opt/gcc-linaro-arm-linux-gnueabihf/bin/arm-linux-gnueabihf- 
# this command takes the existing exynos_defconfig and copies it as .config to the 
# out directory which is then used later on to build the kernel
make O=out exynos_defconfig
# before building, we edit the .config file, there are some drivers we need for the note 10.1
# start the kernel config GUI, I prefer nconfig, there is others, use 'make help' for more
make O=out nconfig
# we have everything in place, let's build the kernel, the -j parameters tells the compiler
# how many threads to use, nproc --all returns the number of processors in the system
make O=out -j$(nproc --all) 
```

The build usually only takes a couple of minutes on current hardware, from the result there are two files of interest:

* out/arch/arm/boot/zImage
* out/arch/arm/boot/dts/exynos4412-p4note-n8010.dtb

The first file is the kernel image itself with all the architecture code and drivers that have been selected. It may contain drivers that we don't need, as is the case for the exynos_defconfig. This defconfig file compiles a kernel that can be used across all the existing exynos devices. But then, how does the kernel know which drivers to load? That's where the dtb file comes in. But now we do have a problem. The version of S-BOOT installed on the Exynos4 devices only knows about a kernel image that includes the board init code, it doesn't know how to handle a device tree. Luckily, there is a kernel option for this fallback case: CONFIG_ARM_APPENDED_DTB.

With this enabled, the kernel will look for the DTB file immediately after the kernel code itself. This means that we can do the following to create a kernel image which includes the DTB file at the end:

```shell
cat out/arch/arm/boot/zImage out/arch/arm/boot/dts/exynos4412-p4note-n8010.dtb > zImage-dtb
```

## Conclusion

Going from board file to device tree was an interesting learning experience and it makes sharing device configurations among similar devices an easy process without littering your code with #ifdefs. 

## Resources

* the <a href="https://bootlin.com/docs/" target="_new">training material</a> from bootlin in general
  * in this case the Device Tree 101 presentation from Thomas Petazzoni
* <a href="https://www.youtube.com/watch?v=Sk9TatW9ino" target="_new">Tutorial: Building the Simplest Possible Linux System</a> from Rob Landley