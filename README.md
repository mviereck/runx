# runx - Run Linux GUI applications on MS Windows
`runx` allows to easily run Linux GUI applications and desktops on MS Windows in Cygwin, MSYS2 or WSL.

 - This is especially of interest for [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) in Windows 10 that does not support graphical applications on itself.

*Background*:
 - `runx` starts an X server, either *VcXsrv* or *XWin*, to provide a graphical environment for Linux applications.
 - `runx` creates an authorization cookie to restrict access to the X server to allowed clients only.
 - `runx` runs the desired Linux GUI application with the credentials needed to access the X server.
 
For similar functionality on native Linux systems use [x11docker](https://github.com/mviereck/x11docker) with options `--exe` or `--xonly`.

## Table of contents
 - [Linux environments on MS Windows](#linux-environments-on-ms-windows)
 - [Installation](#installation)
   - [Installation of X server](#installation-of-x-server)
   - [Installation in WSL](#installation-in-wsl)
   - [Installation in Cygwin](#installation-in-cygwin)
   - [Installation in MSYS2](#installation-in-msys2)
 - [GPU hardware acceleration](#gpu-hardware-acceleration)
 - [Usage examples](#Usage-examples)
   - [Providing X server in background](#providing-x-server-in-background)
 - [Output of `runx --help`](#output-of-runx---help)
 - [Screenshot](#screenshot)

## Linux environments on MS Windows
`runx` can run in:
 - [WSL](https://docs.microsoft.com/en-us/windows/wsl/about): Windows subsystem for Linux.
 - [Cygwin](https://www.cygwin.com/): Cygwin is a large collection of Open Source tools which provide functionality similar to a Linux distribution on Windows.
 - [MSYS2](https://www.msys2.org/): MSYS2 is a software distro and building platform for Windows and serves as a base for [git for windows](https://gitforwindows.org/) and [MingW](http://www.mingw.org/). It is mainly used by developers.
   

## Installation
Installation in general:
 - Install an X server, VcXsrv or XWin.
 - Copy `runx` into folder `/usr/local/bin` and make it executeable with `chmod +x /usr/local/bin/runx`.
 - Install dependencies `xauth` and `xwininfo`.
 
### Installation of X server
`runx` needs an [X server](https://en.wikipedia.org/wiki/X_Window_System). Install on MS Windows one or both of:
 - [VcXsrv](https://sourceforge.net/projects/vcxsrv/) to provide X server *VcXsrv*. 
   - Easier to install than *XWin*.
 - [Cygwin](https://www.cygwin.com) with packages `xinit`, `xauth` and `xwininfo`. 
   - This provides X server *XWin* for Cygwin and WSL.
   - *XWin* has a better `--gpu` support than *VcXsrv*.
 
`runx` will automatically use *XWin* if available. You can specify the desired X server with options `--xwin` or `--vcxsrv`. 

### Installation in WSL
 - Run the following commands in WSL/Ubuntu terminal to install `runx` and its dependencies:
   ```
   sudo wget https://raw.githubusercontent.com/mviereck/runx/master/runx -O /usr/local/bin/runx
   sudo chmod +x /usr/local/bin/runx
   sudo apt update
   sudo apt install xauth x11-utils
   ```
   
### Installation in Cygwin
 - Run the Cygwin installer and install packages `xinit`, `xwininfo`, `xauth` and `wget`.
 - In Cygwin terminal run the commands:
   ```
   wget https://raw.githubusercontent.com/mviereck/runx/master/runx -O /usr/local/bin/runx
   chmod +x /usr/local/bin/runx
   ```
   
### Installation in MSYS2
 - In MSYS2 terminal run the commands:
   ```
   mkdir /usr/local/bin
   wget https://raw.githubusercontent.com/mviereck/runx/master/runx -O /usr/local/bin/runx
   chmod +x /usr/local/bin/runx
   ```
 - Constraints in MSYS2: 
   - MSYS2 does not provide `xauth` to create authentication cookies to restrict access to the X server.
For that reason, using `runix` in MSYS2 is possible, but discouraged. 
   - In MSYS2 `runx` only supports X server *VcXsrv*, but not *XWin*.

## GPU hardware acceleration
`runx` supports GPU hardware accelerated graphics with option `--gpu`.
 - GPU access can cause issues with X server *VcXsrv*, especially with NVIDIA cards. For that reason GPU usage is disabled by default in `runx`.
 - If you encounter issues with option `--gpu`, try X server *XWin* instead of *VcXsrv*.

## Usage examples
 - File manager pcmanfm in WSL:
   - Installation:
     ```
     sudo apt update
     sudo apt install pcmanfm
     ```
   - Run:
     ```
     runx -- pcmanfm
     ```
 - Mate desktop environment in WSL:
   - Installation:
     ```
     sudo apt update
     sudo apt install mate-desktop-environment
     ```
   - Run:
     ```
     runx --desktop --gpu -- mate-session
     ```

### Providing X server in background
You can make an entry in the file `~/.bashrc` to have an X server always available.
Possible entry in `~/.bashrc`:
```
source /usr/local/bin/runx
```
In future runs of the terminal you can directly run Linux GUI applications, e.g.:
```
pcmanfm
```

## Output of `runx --help`
```
runx - Run Linux GUI applications on MS Windows.
Provides an X server on MS Windows in Cygwin, MSYS2 or WSL.

Syntax:
  runx [OPTIONS]  --  [COMMAND]

Options:
  -h, --help                   Show this help.
  -d, --desktop                Open a parent window for desktop environments.
  -g, --gpu                    Enable GPU hardware acceleration. Can fail 
                               with NVIDIA cards. Works best with XWin.
      --size WIDTHxHEIGHT      Window size for option --desktop, e.g. 800x600.
      --vcxsrv                 Use X server VcXsrv.
      --xwin                   Use X server XWin.
      --clipboard [=yes|no]    Enable clipboard sharing yes/no. Default: yes.
      --display N              Use display number N for new X server.
      --no-auth                Disable X cookie authentication. Discouraged.
      --cleanup                Stop all X servers and delete cookies.
  -v, --verbose                Be verbose.

Installation of runx in WSL:
 - Copy runx into /usr/local/bin/
 - Make runx executeable:        sudo chmod +x /usr/local/bin/runx
 - Install xauth and xwininfo:   sudo apt update
                                 sudo apt install xauth x11-utils
 
Install an X server on Windows:
  runx supports two X servers: VcXsrv and XWin. Install at least one of them.
   - VcXsrv: Download and install from: 
       https://sourceforge.net/projects/vcxsrv/
   - XWin: Download and install Cygwin64 with packages: xinit xauth xwininfo
       https://www.cygwin.com
VcXsrv is easier to install. XWin provides a better GPU support.

WSL, Cygwin:       runx starts XWin if available, otherwise it starts VcXsrv.
MSYS2 constraints: runx only supports VcXsrv without cookie authentication.

Usage:

Example to directly run an application with runx:
 - Install file manager pcmanfm: sudo apt update
                                 sudo apt install pcmanfm
 - Run pcmanfm with:             runx -- pcmanfm

Example to run Mate desktop:
 - Install Mate desktop with:    sudo apt install mate-desktop-environment
 - Run Mate desktop with:        runx --desktop -- mate-session
 
Example to get a Wayland environment:
 - Install Wayland compositor:   sudo apt install weston
 - Run Weston with:              XDG_RUNTIME_DIR=/tmp  runx -- weston

Providing an X server in background all the time:
 - Create an entry in ~/.bashrc: source /usr/local/bin/runx
 - In future terminal session you can directly run GUI commands.
   E.g. just type:  'pcmanfm'  instead of 'runx -- pcmanfm'.
 ```
 
 ## Screenshot
 `runx` running Mate desktop on MS Windows:
 ![Mate Desktop on MS Windows](https://raw.githubusercontent.com/mviereck/x11docker/screenshots/screenshot-runx.png)
 
