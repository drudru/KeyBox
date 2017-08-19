# Installation Instructions

Currently the system is based on the Raspbian Jessie Lite distribution. In the near future
there will be a small image that will just unzip and have all the necessary software.

## Networked Portion

Install that first onto a microSD card and hook it up to a raspberry pi.

You will need network connectivity on the pi in order to complete the following Steps. In my case, I had a Pi Zero,
so I needed to add networking. With a Pi Zero W, you can probably use WiFi.
I used an adafruit 'Tiny OTG Adapter' and a TrendNet USB 3.0 to gigabit Ethernet adapter. Be sure to plug the network into the port
labeled USB instead of PWR.

You will then need to install some additional packages via 'apt-get'. You can either put the deb packages on the 
microSD or connect a USB network device in order to download the deb packages.

* wiringpi
* fgetty
* runit
* ipsvd

Because we need to emulate more than one USB device, we need to use a composite USB setup that is not commonly
described on the internet. Most online guides describe how to setup a device into a gadget mode, but for only one
gadget. This setup uses the more modern approache that the linux kernel community has built into the kernel about 5? years ago.

Unfortunately, due to a bug in the most recent raspbian jessie Linux kernel, using the gadget mode causes an exception.
Here is the linked bug: [Issue #1943](https://github.com/raspberrypi/linux/issues/1943).

The fix is to run 'raspi-update' as root to get the latest patched kernel.

There are three config files in this git repo which need to be put into place over the TODO

You need to install the following packages from the repos here on github : TODO

## Standalone Portion

At this point, you should have all the software and configuration files set-up on the device.
The device will act as a USB HID (Keyboard, Mouse, etc.) and a network device.

You should now unplug all power and plug only your mini-USB cable into the port labeled USB on the Pi.
This will power-up your KeyBox and also allow your Pi to emulate USB devices.



