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

### Set-Up Alire
setup Alire by pointing to the Alire page

### Install the Build Essentials
W: install Msys2 or configure Alire to use preinstalled Msys2
L: apt install build-essentials, git

### Install the Debugger OpenOCD
https://openocd.org/

V0.12 does not need a patch anymore


#### Install Software on Windows
msys2: pacman

#### Install Software on Linux
apt install openocd

https://wiki.debian.org/OpenOCD


#### Wiring
Second RPi Pico as debugger, which ports to connect

build separate debug probe 

#### Install Software on Probe

### Select Tool-Chain

alr toolchain --select

### Select an IDE (VSCode and Emacs with Ada-Mode)

### Create the Initial Frame for Your Own Project

### Look at Other Examples
