# Pico-Setup-Ada
Description how to set up an Ada development environment for Raspberry Pico or similar rp2040/rp2350 boards

create separate pages for Windows and Linux or do it in parallel?

```mermaid
flowchart LR
    id1[Alire]
    id2[Build Essentials]
    id3[OpenOCD]
    id4[Toolchain]
    id5[IDE]
    id1 --> id2 --> id3 --> id4 --> id5
```

## Set-Up Alire
Alire is the Ada package manager. It manages dependancies between libraries and tools. Download the latest version from their Github [repository](https://github.com/alire-project/alire/releases). 

### Windows
The installer creates a desktop icon that starts a Powershell. The `PATH` is automatically extended for the `alr` binary. 

### Linux
The downloaded archive essentially contains the only file `bin/alr`. You better extract it being in your home directory. The installation path `~/bin/` is already in your `PATH` most probably.

## Install the Build Essentials

You need several other tools and libraries besides a compiler and an editor like `make`, `git` for version control, `unzip`, `libusb`, etc. 

### Windows
On the first invocation of `alr` it proposes to download [Msys2](https://www.msys2.org/) and associated tools for you.  If you already have Msys2 you can [configure](https://alire.ada.dev/docs/#alr-on-windows) Alire to use the preinstalled Msys2. In that case I recommend to add the Alire installation directory to you `PATH`, e.g. in your `.profile`.

### Linux
Linux already has all the necessary tools.  In case you are missing something install it with your Linux package manager.
```shell
$ apt install build-essentials, git
```

## Install the Debugger OpenOCD
The standard way to install your binaries on the Pico board is to copy an uf2 file to it. I highly recommend, however, to use a debugger via the Serial Wire Debug (SWD) interface.  You need the software [OpenOCD](https://openocd.org/) and a second Pico.

### Install Software on Windows

```shell
pacman -S mingw-w64-ucrt-x86_64-openocd
```

### Install Software on Linux

```shell
apt install openocd
```

https://wiki.debian.org/OpenOCD


### Hardware Wiring for a Seconds Pico as Debug Probe
Second RPi Pico as debugger, which ports to connect

build separate debug probe 

### Install Software on Probe
https://raspberry-projects.com/pi/microcontrollers/programming-debugging-devices/debugging-using-another-pico

## Select Tool-Chain

alr toolchain --select

## Select an IDE (VSCode and Emacs with Ada-Mode)

## Create the Initial Frame for Your Own Project

## Look at Other Examples
