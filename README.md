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
The standard way to install your binaries on the Pico board is to copy an uf2 file to it. I highly recommend, however, to use a debugger via the Serial Wire Debug (SWD) interface.  You first need the software [OpenOCD](https://openocd.org/) and a second Pico that works as a debug probe. The standard package managers for Windows and Linux provide at least version 0.12 that works with the rp2040 chips. Second you need the GNU debugging program `gdb`.

The stock OpenOCD distributions V0.12 (Windows and Linux as well) has a nasty bug in that stops timers. See [here](https://github.com/raspberrypi/pico-sdk/issues/1622). A solution is the upstrewam sources and in the fork of the Raspberry Foundation. Perhaps there is also a version of OpenOCD that gets installed through the VSCode extension that does not show the problem, to be confirmed. 

### Install Software on Windows

```shell
pacman -S mingw-w64-ucrt-x86_64-openocd
pacman -S mingw-w64-ucrt-x86_64-gdb
```


#### USB Driver

As explained in the official guide, you need to make sure that the right USB drivers are being used. Download Zadig from http://zadig.akeo.ie and run it. First select `Options / List all devices` from the menu. Then you can chose `Picoprobe (Interface 2)` and make sure it's using the `libusb-win32` driver.

![Zadig](img/image.png)

### Install Software on Linux

```shell
apt install openocd gdb
```
You can find further information about OpenOCD on Debian at their [wiki](https://wiki.debian.org/OpenOCD).


### Seconds Pico as Debug Probe
See the setup guide on how to install software and how to wire the second Pico board.


## Select Tool-Chain
```
alr toolchain --select
```

## Select an IDE (VSCode and Emacs with Ada-Mode)

## Create the Initial Frame for Your Own Project

## build the sample program

## Debug the Sample Program

### upload program

```
openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -s tcl -c "program test.elf verify reset exit"
```

### Start OpenOCD for Debugging
```
openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -s tcl -c "set USE_CORE 0" -c "adapter speed 5000"
```

`set USE_CORE 0` should circumvent a problem when debugging timers
`adapter speed 5000` increases communication speed to the target

Another workaround is to set `timer_hw->dbgpause` (what is that in Ada?) to `0` in your startup code.


## Look at Other Examples
