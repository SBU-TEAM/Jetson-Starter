# Jetson Nano StartUp Levels

* [Setup SD card](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-sd-card)
* [Boot Jetson](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#boot-jetson)
* [Setup VPN](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-vpn)
* [Update Packages](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#update-packages)
* [Check Swap](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#check-swap)
* [Install packages](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#install-packages)
* [Setup VNC](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-vnc)
* [Enable light mode](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#Enable-light-mode)
* [Connect to jetson via SSH](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#Connect-to-jetson-via-SSH)

# Setup SD card

Download [Jetpack Image file](https://ln5.sync.com/dl/741c98fe0/x8kxkhgs-cgmzk7rf-n4m7pyw8-h64tzbv5/view/default/11304846510004).
<br>One **32GB** SD card is needed. Format SD card; use [SD card formatter](https://www.sdcard.org/downloads/formatter/) in this case.
<br>Download [balenaEtcher](https://www.balena.io/etcher). Write Jetpack Image file on the SD card with blenaEtcher, wait until validation is done.

>[*more information*](https://github.com/Qengineering/Jetson-Nano-Ubuntu-20-image)

# Boot Jetson

Place SD card in the Jetson and Turn in On (Connect the power jack).

>**Its DONE :)**

# Setup VPN

# Update Packages

Update packages links with `apt`

    sudo apt update
  
Upgrade packages, this will take some time

    sudo apt upgarde

Freeup some space

    sudo apt autoremove
    
# Check Swap

The swap memory method in use is Zram. You can examine the swap memory information

    zramctl

>if there is less than 4G of swap memory, increase it with help of [resizeSwapMemory](https://github.com/JetsonHacksNano/resizeSwapMemory).

# Install packages

#### install `zsh`, `git` and `curl`

    sudo apt install zsh git curl
   
install `oh my zsh` with `curl`

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     
Download zsh-autosuggestions by

    git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
    
Download zsh-syntax-highlighting by

    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

add plugins in `.zshrc`

    nano ~/.zshrc
    
>find `plugins=(git)`, edit to `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`
<br>find `ZSH_THEME="shit"`, edit to `ZSH_THEME="eastwood"`

Set `zsh` system default shell

    sudo chsh -s /bin/zsh jetson

>**reboot**

>[*more information*](https://gist.github.com/dogrocker/1efb8fd9427779c827058f873b94df95)
---
#### install vscode 

downlaod [vscode](https://code.visualstudio.com/download), get `.deb` file for `Arm64`.

install `code` with `apt`

    sudo apt install ./vscode_file_name.deb
    
open vscode after installation
    
    code
    
>[*more infortmation*](https://code.visualstudio.com/docs)

# Setup VNC

Update packages links with `apt`

    sudo apt update
 
Install Xfce along with the `xfce4-goodies` package, which contains a few enhancements for the desktop environment
 
    sudo apt install xfce4 xfce4-goodies
    
Once that installation completes, install the `TightVNC` server

    sudo apt install tightvncserver
    
Run the vncserver command to set a VNC access password(The password must be between six and eight characters long)

    vncserver
    
Once you verify the password, you’ll have the option to create a view-only password: answer `no`

The password can be changed

        vncpasswd

Before you modify the `xstartup` file, back up the original


    mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
    
Now create a new `xstartup` file and open it in a text editor, such as `nano`
    
    nano ~/.vnc/xstartup
    
Then add the following lines to the file

    #!/bin/bash
    xrdb $HOME/.Xresources
    startlxde &
    
To ensure that the VNC server will be able to use this new startup file properly, you’ll need to make it executable

    chmod +x ~/.vnc/xstartup
    

# Enable light mode

Lightdm boot mode or `lxde` (Lightweight X11 Desktop Environment) will save 1Gb of RAM.

    sudo dpkg-reconfigure lightdm
        
A window will pop up, there are two options: `gdm3` and `lightdm`, select `lightdm` and press enter.

>**reboot**

for returning to gdm3 boot mode

    sudo dpkg-reconfigure gdm3
        
>[*more information*](https://jetsonhacks.com/2020/11/07/save-1gb-of-memory-use-lxde-on-your-jetson/)

# Connect to Jetson via SSH

To connect to SSH via LAN, connect a LAN cable to your labtop and jetson nano.Then go to the `Network Setting` of your Ubuntu.Hit the `setting` button of Wired Connection.
In `Ipv4` section change the form of connection to `share to other computers`.Then restart the connection.You should be able to connect to jetson now.
