# runx
```
runx - Provide an X server on MS Windows in WSL, Cygwin or MSYS2
Run Linux GUI applications on MS Windows.

Syntax:
  runx [OPTIONS]  --  [COMMAND]

Options:
  -h, --help                     Show this help.
  -d, --desktop                  Open a parent window for desktop environments.
  -g, --gpu [=yes|no]            Enable GPU hardware acceleration. Default: no.
                                 Can fail with NVIDIA cards.
  -c, --clipboard [=yes|no]      Enable clipboard sharing yes/no. Default: yes.
      --display N                Display number N for new X server.
      --no-auth                  Disable X cookie authentication. Discouraged.
  -v, --verbose                  Be verbose.

Installation:
 - Copy runx into /usr/local/bin/
 - Make runx executeable:        sudo chmod +x /usr/local/bin/runx
 - Install xauth and xwininfo:   sudo apt install xauth x11-utils
Install on Windows:
 - Download and install X server VcXsrv from: 
     https://sourceforge.net/projects/vcxsrv/

Usage:
You can create an entry in ~/.bashrc to always have an X server available.
Possible entry in ~/.bashrc:     source /usr/local/bin/runx

Example to run an application directly with runx:
 - Install file manager pcmanfm: sudo apt update
                                 sudo apt install pcmanfm
 - Run pcmanfm with:             runx -- pcmanfm

Example to run Mate desktop:
 - Install Mate desktop with:    sudo apt install mate-desktop-environment
 - Run Mate desktop with:        runx --desktop -- mate-session
 ```
 
