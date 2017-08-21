
KeyBox Project
--------------

The KeyBox project combines a Raspberry Pi Zero, a small TFT display, and some software
into a device that holds passwords and cryptographic keys.

<img src="Images/Front.jpg" width="320" height="240" /> <img src="Images/Back.jpg" width="320" height="240" />

The will hold your passwords and allow you to play them back by emulating a USB keyboard.

The device will also emulate and ssh-agent and allow you to keep all of your ssh keys
securely on this device.

This is the central repository for the KeyBox project.
It will have pointers to other repos necessary to build the KeyBox distribution.

* [kb-gui](https://github.com/drudru/kb-key) - presents UI on tft
* [kb-key](https://github.com/drudru/kb-key) - sends emulated keystrokes

All software should be under an MIT or similar open source license.

If you have any questions, please open an issue.

[Installation Instructions](Install/INSTALL.md)

[Build Instructions](Build/BUILD.md)

2017-08-17 - Just read that new RASPBIAN STRETCH LITE has been released.
For now, I am working on a Jessie image, but I will build a new image based on Stretch.
Also, I will upload instructions on how to build an image today.

## Hardware

The key to KeyBox is the fact that the Raspberry Pi 0 connects its USB hardware directly to 
the USB ports. This allows it to emulate USB devices via USB On-The-Go.
The Raspberry Pi 2/3 connect these to a USB hub which prevents this.

* Raspberry Pi 0
  * Probably supports Pi 0 W or Pi A+ - not tested
* Adafruit 2.2" TFT HAT
  * Has 4 buttons. Requires little soldering.
* Piezo Buzzer
* 3D Case
  * I don't have a 3D printer or case design currently.
  
There will be a separate section that can go into more details about the hardware and 
support for other platforms (BeagleBone, Arduino, etc.)

## License

I will add the license files, but everything in this repo is under a BSD or MIT license.




