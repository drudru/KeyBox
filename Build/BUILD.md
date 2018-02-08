# Build Instructions

All of the binaries for KeyBox are written in C++. This document describes how to compile
the C++ into the binaries for the device.

## Build Environment

### Hardware

I don't recommend building on a Raspberry Pi 0.

I recommend a separate 'desktop' class Unix system to be able to cross-compile.

I also **highly** recommend a reliable USB serial device that can communicate at 115200 bps to the Raspbery Pi. I used
a Bus Pirate from Dangerous prototypes without issue. Without a serial console, it is very difficult to see what is going
on with the device.

### Software

I am currently building the binaries on my Mac OS X system. However, you can use any environment
that supports the following tools.

* git
* [fips](https://github.com/floooh/fips)
  * CMake
  * python3
  * [ninja](https://ninja-build.org/) - OPTIONAL - a fast build system
* [crosstool-NG](https://crosstool-ng.github.io/)
  * An existing C/C++ compiler will be needed to build crosstool-NG
  * See the crosstool-NG site for more of its requirements

I recommend creating a single directory where all this software will be installed.
This is where you will have fips, crosstool-NG, and the cloned KeyBox git repos.
If you have an existing Project directory where you normally do your work, *I do not recommend* cloning these repos
into it.
If you install fips there, it will put a lot of new subdirectories where you may not expect them.

If you are on a Mac, the requirement is even stricter. You will need to build a CASE-SENSITIVE disk image with the disk utility. Instructions on how to do this are on the net. I created a 16GB image. Once you do this, perform all of the work in
this newly created mounted volume. I called my volume 'crosstools'. If you name yours that, you will have to do
less configuration.

I also recommend adding '.' to your PATH environment variable. This will make fips commands a little more convenient.

### fips

**fips** is sort of like npm for C++. All of the C++ projects share code via fips.
See the site above for install instructions.

### crosstools-NG

You will 
crosstools-NG will set up an entire cross compiler toolchain. Specifically this will be the GCC compiler,
linker, assembler, binutils, etc. It will also build a glibc. I recommend building to a 4.9 version of the
Linux kernel.

You can do all of this via the 'ct-ng menuconfig' command.

The target architecture is Linux 32 bit armhf.

This [link](http://www.bootc.net/archives/2012/05/26/how-to-build-a-cross-compiler-for-your-raspberry-pi/) has good instructions on the configuration of crosstool-NG for an armhf build.

The binaries for my crosstools-NG install are in: /Volumes/crosstools/x-tools/


### Performing a build

Once you have the above all installed, it is time to combine them together.
We will need to configure fips to use the crosstool-NG as the compiler.

The first thing you will need to do is to change the paths in your 'fips-toolchains/xpi0.toolchain.cmake' file.

Once you do that, set the configuration to:

$ fips set config xpi0-ninja-debug

Here are my current settings.


```

$ fips list settings
=== settings:
  config: xpi0-ninja-debug
  target: None (default value)
    jobs: 3 (default value)
  ccache: off
```

Once that is complete you build in each directory by typing: 'fips build'.

If the compile is successful, the binaries will be placed in the fips-deploy directory.

For example, on my system the kb-gui binary is placed in:
/Volumes/crosstools/fips-deploy/kb-gui/xpi0-ninja-debug/kb-gui

If you add files to the project, you may need to run 'fips gen' in order to have
CMake build new ninja build files.

