# runx
```
runx - Provide an X server on MS Windows in WSL, MSYS2 or Cygwin
Run Linux GUI applications on MS Windows.

Syntax:
  runx [OPTIONS]  --  [COMMAND]

Options:
  -h, --help                     Show this help.
  -d, --desktop                  Open a parent window for desktop environments.
  -g, --gpu [=yes|no]            Enable GPU hardware acceleration. Default: no.
                                 Can fail with NVIDIA cards. Works better with
                                 XWin in Cygwin than with VcXsrv.
  -c, --clipboard [=yes|no]      Enable clipboard sharing yes/no. Default: yes.
      --display N                Display number N for new X server.
      --no-auth                  Disable X cookie authentication. Discouraged.
      --cleanup                  Stop all X servers and delete cookies.
  -v, --verbose                  Be verbose.

Installation in WSL, MSYS2 or Cygwin:
 - Copy runx into /usr/local/bin/
 - Make runx executeable:        sudo chmod +x /usr/local/bin/runx
 - Install xauth and xwininfo:   sudo apt install xauth x11-utils
Install on Windows:
 - Download and install X server VcXsrv from: 
     https://sourceforge.net/projects/vcxsrv/
(In Cygwin you can install XWin (package xinit) instead of VcXsrv.)

Usage:
You can create an entry in ~/.bashrc to always have an X server available.
Possible entry in ~/.bashrc:     source /usr/local/bin/runx

Example to directly run an application with runx:
 - Install file manager pcmanfm: sudo apt update
                                 sudo apt install pcmanfm
 - Run pcmanfm with:             runx -- pcmanfm

Example to run Mate desktop:
 - Install Mate desktop with:    sudo apt install mate-desktop-environment
 - Run Mate desktop with:        runx --desktop -- mate-session
 ```
 
