# runx
```
runx - Provide an X server on MS Windows in Cygwin, MSYS2 or WSL.
Run Linux GUI applications on MS Windows.

Syntax:
  runx [OPTIONS]  --  [COMMAND]

Options:
  -h, --help                     Show this help.
  -d, --desktop                  Open a parent window for desktop environments.
  -g, --gpu [=yes|no]            Enable GPU hardware acceleration. Default: no.
                                 Can fail with NVIDIA cards. Works better with
                                 XWin in Cygwin than with VcXsrv.
      --clipboard [=yes|no]      Enable clipboard sharing yes/no. Default: yes.
      --vcxsrv                   Use X server VcXsrv.
      --xwin                     Use X server XWin.
      --display N                Display number N for new X server.
      --no-auth                  Disable X cookie authentication. Discouraged.
      --cleanup                  Stop all X servers and delete cookies.
  -v, --verbose                  Be verbose.

Installation of runx in WSL, MSYS2 or Cygwin:
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
You can create an entry in ~/.bashrc to always have an X server available.
In that case you don't need to type 'runx' anymore.
Possible entry in ~/.bashrc:     source /usr/local/bin/runx

Example to directly run an application with runx:
 - Install file manager pcmanfm: sudo apt update
                                 sudo apt install pcmanfm
 - Run pcmanfm with:             runx -- pcmanfm

Example to run Mate desktop:
 - Install Mate desktop with:    sudo apt install mate-desktop-environment
 - Run Mate desktop with:        runx --desktop -- mate-session
 ```
 
