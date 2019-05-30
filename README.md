# runx
```
runx - Provide an X server in WSL.
Run Linux GUI applications on MS Windows.
 
Syntax:
  runx [OPTIONS] [ -- ] [COMMAND]

Options:
  -h, --help                     Show this help.
  -d, --desktop                  Open a parent window for desktop environments.
  -g, --gpu [=yes|no]            Enable GPU hardware acceleration. Default: no.
                                 Can fail with NVIDIA cards.
  -a, --no-auth                  Disable X cookie authentication. Discouraged.
  -c, --clipboard [=yes|no]      Enable clipboard sharing yes/no. Default: yes.
  -v, --verbose                  Be verbose.

Installation:
In WSL:
 - Copy runx into /usr/local/bin/
 - Make runx executeable:        sudo chmod +x /usr/local/bin/runx
 - Install xauth and xwininfo:   sudo apt-get install xauth x11-utils
On Windows:
 - Download and install X server VcXsrv from: 
     https://sourceforge.net/projects/vcxsrv/
   
You can create an entry in ~/.bashrc to always have an X server available.
Possible entry in ~/.bashrc:     source /usr/local/bin/runx

Example to run an application directly with runx:
 - Install file manager pcmanfm: sudo apt update
                                 sudo apt install pcmanfm
 - Run thunar with:              runx pcmanfm
 
Example to run Mate desktop:
 - Install Mate desktop with:    sudo apt-get install mate-desktop-environment
 - Run Xfce with:                runx --desktop startxfce4
 ```
 
