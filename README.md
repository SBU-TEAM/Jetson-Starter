# Jetson Nano StartUp Levels

* [Setup SD card](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-sd-card)
* [Boot Jetson](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#boot-jetson)
* [Setup VPN](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-vpn)
* [Update Packages](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#update-packages)
* [Check Swap](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#check-swap)
* [Install packages](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#install-packages)
* [Setup VNC](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#setup-vnc)
* [Enable light mode](https://github.com/SBU-TEAM/Jetson-Starter/blob/master/README.md#Enable-light-mode)

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

### install `zsh`, `git` and `curl`

    sudo apt install zsh git curl
---    
### install `oh my zsh` with `curl`

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     
Download zsh-autosuggestions by

    git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
    
Download zsh-syntax-highlighting by

    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

add plugins in `.zshrc`

    nano ~/.zshrc
    
find `plugins=(git)`, edit to `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`.

>[*more information*](https://gist.github.com/dogrocker/1efb8fd9427779c827058f873b94df95)
---
### install vscode 

downlaod [vscode](https://code.visualstudio.com/download), get `.deb` file for `Arm64`.

install `code` with `apt`

    sudo apt install ./vscode_file_name.deb
    
open vscode after installation
    
    code
    
>[*more infortmation*](https://code.visualstudio.com/docs)

# Setup VNC

# Enable light mode

Lightdm boot mode or `lxde` (Lightweight X11 Desktop Environment) will save 1Gb of RAM.

    sudo dpkg-reconfigure lightdm
        
A window will pop up, there are two options: `gdm3` and `lightdm`, select `lightdm` and press enter.

>**reboot**

for returning to gdm3 boot mode

    sudo dpkg-reconfigure gdm3
        
>[*more information*](https://jetsonhacks.com/2020/11/07/save-1gb-of-memory-use-lxde-on-your-jetson/)

