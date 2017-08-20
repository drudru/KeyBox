# Build Instructions

All of the binaries for KeyBox are written in C++. This document describes how to compile
the C++ into the binaries for the device.

## Build Environment

I don't recommend building on a Raspberry Pi 0.

I am currently building the binaries on my Mac OS X system. However, you can use any environment
that supports the following tools.

* git
* [fips](https://github.com/floooh/fips)
  * CMake
  * python3
  * [ninja](https://ninja-build.org/) - OPTIONAL - a fast build system
* [crosstool-NG](https://crosstool-ng.github.io/)

I recommend creating a single directory where all this software will be installed.
This is where you will have fips, crosstool-NG, and the cloned KeyBox git repos.
If you have an existing Project directory where you normally do your work, *I do not recommend* cloning these repos
into it.
If you install fips there, it will put a lot of new subdirectories where you may not expect them.

If you are on a Mac, the requirement is even stricter. You will need to build a CASE-SENSITIVE disk image with the disk utility. Instructions on how to do this are on the net. I created a 16GB image. Once you do this, do all of the work in
this mounted volume.

I also recommend adding '.' to your PATH environment variable. This will make fips commands a little more convenient.

### fips

**fips** is sort of like npm for C++. All of the C++ projects share code via fips.
See the site above for install instructions.

### crosstools-NG

crosstools-NG will set up an entire cross compiler toolchain. Specifically this will be the GCC compiler,
linker, assembler, binutils, etc. It will also build a glibc.

The target architecture is Linux 32 bit armhf.

This [link](http://www.bootc.net/archives/2012/05/26/how-to-build-a-cross-compiler-for-your-raspberry-pi/) has good instructions on the configuration of crosstool-NG for an armhf build.


### Performing a build

Once you have the above all installed, it is time to combine them together.
We will need to configure fips to use the crosstool-NG as the compiler.

TODO: describe this config in detail

Here are my current settings.

$ fips list settings

=== settings:
  config: xpi0-ninja-debug
  target: None (default value)
    jobs: 3 (default value)
  ccache: off



Once that is complete you generate the Ninja/Make/etc. files by typing typing: 'fips gen'.

Once that is complete you build in each directory by typing: 'fips build'.

If the compile is successful, the binaries will be placed in the fips-deploy directory.

For example, on my system the kb-gui binary is placed in:
/Volumes/crosstools/fips-deploy/kb-gui/xpi0-ninja-debug/kb-gui


