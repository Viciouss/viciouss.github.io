---
layout: post
title: The Boot Image
date: 2022-01-24 20:00:00 +0200
---

## Get to know your Boot Image

To boot the device with S-Boot as boot loader, you need to provide an image that has a special format. This format is described on the <a href="https://source.android.com/devices/bootloader/boot-image-header" target="_new">Boot Image Header</a> page of the AOSP project. In our case, as the device was released with Android 4, this is the legacy header or version 0. It contains the following entries:

* kernel image size and address
* ramdisk size and address
* second bootloader size and address
* some meta data

The interesting part here is the kernel image and ramdisk, on the Galaxy Note 10.1 the second stage boot loader (S-Boot) is not part of the boot image. It resides on its own partition.

## Creating a Boot Image

Fortunately, there is a tool to extract and assemble boot images for Android. It's called **abootimg** and can be installed with the package manager on probably any of the popular linux distros. The man page should provide enough information to understand how it works.

What is not explained in detail is the boot image configuration file format. What does it look like? As I mentioned, you can extract boot.img files, so for your device this would be the way to go. Looking at the cfg file for the Note 10.1 and the AOSP description of the header format, you will probably see where this goes:

```shell
bootsize = 8388608
pagesize = 0x800
kerneladdr = 0x40008000
ramdiskaddr = 0x42000000
secondaddr = 0x40f00000
tagsaddr = 0x40000100
name = 
```

With this information, a sample call to create a boot.img for my case looks like this:

```shell
abootimg --create myboot.img \
        -f bootimg.cfg
        -r ramdisk.xyz
        -k zImage-dtb
```

## Bootloader and the Boot Image

Now that you know how the image looks like, let's have a look at the boot process, especially how the boot image is taken care off.

The second stage boot loader first looks at the boot partition and the boot image header. Depending on the numbers you provided, it puts everything in the right place in the memory of your device and then calls the kernel image entry point. As the device is from 2012 and neither uses nor supports a Device Tree entry in the boot image, parameters are still fed to the kernel with the ATAGS mechanism - that's what the **tagsaddr** attribute is for.

The ATAGS or kernel tagged list is an area in RAM where the boot loader puts parameters for the kernel to consider. There is a hand full of parameters, from memory size and location, ramdisk size and location to serial number, revision and command line. The bootloader then puts the address of this list into the R2 register, next to the R1 register which contains the machine type id. Only with those two pieces of information, the kernel can chose the right path of what to do next.

Technically, you don't need the R1 and R2 registers and the parameters from the kernel tagged list, as the Device Tree describes all necessary parameters for a specific device. Remember the config option to attach the DTB file at the end of the kernel? That's what will work for the mainline kernel. Nevertheless, it is interesting to have these parameters from the boot loader to build the device tree in the first place.

Let's have a look at what they are for the Note 10.1 and how the vendor boot image deals with them:

```text
ATAG_CORE: 5 54410001 0 0 0
ATAG_MEM: 4 54410002 20000000 40000000
ATAG_MEM: 4 54410002 20000000 60000000
ATAG_MEM: 4 54410002 20000000 80000000
ATAG_MEM: 4 54410002 1FC00000 A0000000
ATAG_SERIAL: 4 54410006 aaaaaaaa aaaaaaaa
ATAG_INITRD2: 4 54420005 42000000 3a50bc
ATAG_REVISION: 3 54410007 6
ATAG_CMDLINE: ad 54410009 'console=ttySAC2,115200 loglevel=4 bootmode=2 sec_debug.level=0 sec_watchdog.sec_pet=5 androidboot.debug_level=0x4f4c sec_log=0x200000@0x46000000 sec_tima_log=0x200000@0x46202000 sec_avc_log=0x40000@0x46404000 s3cfb.bootloaderfb=0x5ec00000 sysscope=0xee000000 lcdtype=1 consoleblank=0 lpj=3981312 vmalloc=256m oops=panic pmic_info=1 cordon=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa connie=GT-N8000_OPEN_EUR_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa androidboot.emmc_checksum=3 androidboot.odin_download=1 androidboot.bootloader=N8000XXSDQA7 androidboot.selinux=enforcing androidboot.warranty_bit=0 androidboot.sec_atd.tty=/dev/ttySAC2 androidboot.serialno=aaaaaaaaaaaaaaaa snd_soc_core.pmdown_time=1000'
ATAG_NONE: 0 0
```

ATAG_MEM - describes the ram in four banks of 512 MiB each. The last one is actually 4 MiB short, my guess is that this is related to the bootloader process.

ATAG_SERIAL - the serial number of the device.

ATAG_INITRD2 - is set to the memory position of the ramdisk that was written to the boot.img configuration with **abootimg**.

ATAG_REVISION - holds a revision number which is used in several places in the vendor kernel to distinguish some board details.

ATAG_CMDLINE - again rather obvious.

ATAG_NONE - the end of the tagged list.

About the revision, this comes to play in <a href="https://github.com/Viciouss/samsung_p4note_kernel_backup/blob/da306e1846bb4b9682f46be1b23b05d6fbebffba/arch/arm/mach-exynos/p4note-gpio.c#L609" target="_new">GPIO configuration</a>, <a href="https://github.com/Viciouss/samsung_p4note_kernel_backup/blob/da306e1846bb4b9682f46be1b23b05d6fbebffba/arch/arm/mach-exynos/midas-sensor.c#L287" target="_new">sensor positions</a> or even which <a href="https://github.com/Viciouss/samsung_p4note_kernel_backup/blob/da306e1846bb4b9682f46be1b23b05d6fbebffba/arch/arm/mach-exynos/p4-input.c#L747" target="_new">touch screen IC</a> is installed. Although both ot the ICs are actually enabled in the defconfig, I've never come across one of the international versions of this device that haven't had the Atmel IC. The Synaptics touch screen might have been in a prototype version or maybe one of the <a href="https://redmine.replicant.us/projects/replicant/wiki/Exynos4412Devices#Galaxy-Note-101-2012-Edition" target="_new">many variants</a> of the South Korean market which I haven't been able to spot on any hardware info sites yet.

After evaluating all those parameters and finishing loading the kernel, the <a href="https://www.kernel.org/doc/html/latest/admin-guide/initrd.html" target="_new">initrd logic</a> will be executed on the vendor kernel. The ramdisk will be mounted at root and then the kernel runs /sbin/init. As this is already Android territory, we are done here.

As usual, the kernel docs have some more on booting ARM, e.g. the <a href="https://www.kernel.org/doc/Documentation/arm/Booting" target="_new">ARM boot documentation</a>.

## Resources

* the original <a href="https://github.com/Viciouss/samsung_p4note_kernel_backup" target="_new">vendor sources</a> I requested from the <a href="https://opensource.samsung.com/" target="_new">Samsung Open Source</a> page.