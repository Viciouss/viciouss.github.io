---
layout: post
title: Can I has Android now pls?
date: 2023-06-20 23:00:00 +0200
---

## Next Steps

There is a kernel image which might or might not boot, it has the device tree attached at the end of it, the inner workings of the boot image and the bootloader are no longer a mystery. Sounds like everything is in place to assemble the boot image, put it on the device and boot right into Android, right? Well, I have to tell you something.

Android has a history of heavily modifying the mainline kernel, introducing new and changing existing code. When the p4note device family was still new and shiny, there were hundreds of patches on top of mainline. This modified kernel is called the Android common kernel. These kernels were then picked up by the vendors who put another couple of hundred patches on top to get a device up and running. The end result were kernel trees that went up to hundreds of thousands of lines of code away from mainline. Upgrading from an old downstream kernel to mainline is therefor guaranteed to fail miserably. The system and vendor userspace parts (like the Android HAL and vendor binaries) expect certain files to exist, like sysfs and devfs entries, as well as certain uevents to be triggered. All this is missing.

Building Android from scratch is quite a huge task as well. It's not like throwing in a kernel and then building it, the hardware abstraction layer will kick your butt if you are missing a required implementation for memory management, graphics and other things. A lot of configuration needs to be done before an image even comes out at the end of the build process. This is putting way too much complexity on top and with drivers missing, it will be an awful user experience anyway.

Ok then, how about starting small? There are a couple of options to chose from. The simplest solution is compiling a little init program to print out a hello world and packaging it with the kernel. But what to do with it next?

Maybe grabbing a copy of <a href="https://www.busybox.net/" target="_new">busybox</a> and assembling a small system with a shell sounds great? For sure it does, but the goal is to write more driver code and not setting up an embedded system from scratch with half the drivers not working. So how about something more "usable" with tools already available?

Luckily, there are projects that provide small base systems with lots of customization options. They will provide a wide range of libraries and programs to be included in a linux system. Those projects also have build systems in place that will pick up all the tedious work and throw out a boot and system image at the end. Let's have a look at one of them.

## Introducing Buildroot

I chose buildroot for no apparent reason, I liked the name and it looked easy to get started with, so I just went with it.

So what is buildroot? It's basically a collection of Make files, package descriptions and patches that, combined with a config file, will assemble a custom root filesystem tailored to your specific needs. There are hundreds of software packages to chose from and it uses the Linux kernel kconfig system for configuration. Sounds great for mainline development!

## Buildroot in 10 Minutes

First, let's download a copy of <a href="https://www.buildroot.org/download.html" target="_new">Buildroot</a>. Anything not too old will be fine for this example. For the p4note project (see the end of this post), at least version 2023.02 is required for the 6.1 mainline kernel that is used.

To work with buildroot, there needs to be a board description for the target. This is either located in buildroot itself if it is officially maintained or in a so called external tree in a separate directory/repository. The board description usually contains config files and an overlay to the root file system for files that will be packaged along with it. A small skeleton project can be assembled in as little as three files:

* Config.in
* external.mk
* external.desc

A defconfig file describes the selected options in buildroot. It is not mandatory, only the above files are, but for reasons you will see in a minute, it makes sense to already create it:

* configs/p4note_defconfig

Only the external.desc file actually needs content to get started, the other files can be empty. It holds a name and a description for the board. For the p4note, I chose the following:

```
name: P4NOTE
desc: The Samsung Galaxy Note 10.1
```

The name should be A-Z0-9 all caps, as it will be part of the kconfig entries. Lowercase letters are technically allowed, but who would do such cruel thing? The description can be freely chosen, but it should fit in one line as it will be displayed in the menuconfig.

With this created, the configuration part can begin. In the buildroot directory, this command will copy the defconfig from the external tree to buildroot:

```
make BR2_EXTERNAL=/path/to/external/tree p4note_defconfig
```

It also sets up the external path as current context. All the following commands can be executed without the BR2_EXTERNAL. The next step is setting the configuration values:

```
make menuconfig
```

There are quite some options to chose from, I will describe the important ones in the next section. Afterwards, use F8 to save to the current file (which is .config in the buildroot dir) and quit.

The changes to the configuration are currently only in the buildroot directory, to finally apply these configuration changes to the external tree, do this:

```
make savedefconfig
```

This will update the defconfig in the configs directory of the external tree, as the current setup has the <a href="https://www.buildroot.org/downloads/manual/manual.html#customize-dir-structure" target="_new">recommended directory structure</a> and that's how buildroot rolls.

As a last step, of course, a call to `make` will build the project.

## Important Configuration

Buildroot uses a lot of sane defaults. It will use the latest available kernel for the buildroot release, recommended build utils, standard libaries and more. Of course there might be differences depending on what you need for your board, but for the p4note I only had to adjust the following:

* Target options
  * all the sub options
* System configuration
  * root password
* Kernel -> Linux Kernel
  * defconfig name, binary format for appended DTB and DTB name
* Filesystem images
  * an ext4 root file system to put the selected packages on

Have a look around, it's not too scary and you should find your way through the menu. After this is done, you can go wild in the `Target Packages` menu, there are a ton of options in there. It's possible to add custom packages in the external tree, have custom pre and post build scripts and more.

## The Final Product

If you navigate to <a href="https://github.com/Viciouss/buildroot_external_p4note" target="_new">https://github.com/Viciouss/buildroot_external_p4note</a>, there is a repository which contains a working configuration with wifi, bluetooth and touch screen already prepared. Wifi and Bluetooth is definitely working for the 3G version (N8000) and should also work for the other two variants, but I haven't tested this.

Don't forget to update wpa_supplicant.conf before building, this way it will connect to your wifi and automatically print the IP on the screen after boot so that you can easily SSH into the device. It will also print the USB ethernet IP as well if your prefer to connect this way. Make sure to change the USB IP of the host machine accordingly.

## Resources

* the <a href="https://www.buildroot.org/downloads/manual/manual.html">buildroot documentation</a> is very good and provides lots of useful information