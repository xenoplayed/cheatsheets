# snapper
sudo pacman -Syu
yay -S btrfs-assistant grub-btrfs snap-pac-git snapper snapper-tools snapper-support

# disable acpi wakeup on usb
echo XHC0 > /proc/acpi/wakeup
echo XHC1 > /proc/acpi/wakeup
echo XHC2 > /proc/acpi/wakeup
echo UXHC > /proc/acpi/wakeup

# GPU
https://wiki.archlinux.de/title/AMDGPU

## install vulkan
vulkan-icd-loader
lib32-vulkan-icd-loader

## install GPU specific vulkan (AMD RADV)
vulkan-radeon
lib32-vulkan-radeon

# gaming?
sudo pacman -Syu --needed steam

# general tools
sudo pacman -Syu --needed vim iproute2 nmap stow zsh flatpak tldr
yay -S reboot-arch-btw

sudo pacman -Syu --needed starship 
sudo pacman -Syu --needed noto-fonts-emoji ttf-firacode-nerd # needed for starship
yay -S ttf-hack-nerd

# localsend
flatpak install localsend
sudo firewall-cmd --zone=public --permanent --add-port=53317/tcp
sudo firewall-cmd --zone=public --permanent --add-port=53317/udp
sudo firewall-cmd --reload

# rustdesk
yay -S rustdesk
sudo firewall-cmd --permanent --add-port=21114-21119/tcp
sudo firewall-cmd --permanent --add-port=21116/udp
sudo firewall-cmd --reload

# yt downloader
sudo pacman -Syu yt-dlp

# brave browser
yay -S brave-bin

# restore dotfiles
cd .dotfiles
stow bash git vim zsh ...

# Package tool (search official, aur and flatpak at once)

# Package GUI (?)
yay -S octopi

# admin tool (https://wiki.archlinux.org/title/Cockpit)
sudo pacman -Syu --needed cockpit cockpit-packagekit firewalld networkmanager kexec-tools
sudo systemctl start cockpit.socket
sudo systemctl enable cockpit.socket

# container (https://wiki.archlinux.org/title/Podman)
sudo pacman -Syu --needed podman podman-docker podman-compose cockpit-podman  # oci-runtime: crun

# virtual machines (https://discovery.endeavouros.com/applications/how-to-install-virt-manager-complete-edition/2021/09/)
sudo pacman -Syu --needed virt-manager qemu-desktop libvirt edk2-ovmf dnsmasq vde2 bridge-utils iptables-nft dmidecode cockpit-machines virt-viewer virt-clone virt-xml virt-bootstrap
sudo systemctl enable --now libvirtd.service
yay -S libguestfs
yay -S qemu-emulators-full

# libvirt networking
sudo virsh net-list --all
sudo virsh net-start default
sudo virsh net-autostart default


# vs code (microsoft, not code oss)
yay -S visual-studio-code-bin

## code extensions
atommaterial.a-file-icon-vscode
file-icons.file-icons
github.copilot
github.copilot-chat
ms-azuretools.vscode-containers
pkief.material-product-icons


atommaterial.a-file-icon-vscode
dart-code.dart-code
dart-code.flutter
file-icons.file-icons
github.copilot
github.copilot-chat
ms-azuretools.vscode-containers
ms-vscode-remote.remote-containers
pkief.material-product-icons


# jetbrains toolbox
yay -S jetbrains-toolbox



## vscode settings

```json
{
  "terminal.integrated.fontFamily": "Hack Nerd Font",
  "editor.fontFamily": "'Hack Nerd Font', Consolas, 'Courier New', monospace"
}

```


# flutter

## prerequisites
sudo pacman -Syu --needed curl git unzip xz zip mesa glu    # dev tools
sudo pacman -Syu --needed glibc gcc-libs zlib bzip2         # to develop android apps

## install flutter from extensions
code --install extension dart-code.flutter 
code --install extension dart-code.dart-code
echo 'export PATH="$HOME/development/flutter/bin:$PATH"' >> ~/.bash_profile # make flutter available from bash
echo 'export PATH="$HOME/development/flutter/bin:$PATH"' >> ~/.zshenv       # make flutter available from zsh

## android
flutter doctor --android-licenses

## desktop-app
sudo pacman -Syu --needed clang cmake git ninja pkgconf gtk3 xz gcc

# AI
## ollama
sudo pacman -Syu --needed ollama-rocm

## ComfyUI

### pyenv
sudo pacman -Syu --needed pyenv

### add to .zshrc / .bashrc
```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```

```shell
# im Home dir
git clone https://github.com/comfyanonymous/ComfyUI.git

# install python 3.12
pyenv install 3.12
cd ComfyUI
pyenv local 3.12

# testen
python -V

```

## LMStudio
# install: https://lmstudio.ai/docs/app/basics

```shell
# Added by LM Studio CLI (lms)
export PATH="$PATH:/home/xeno/.lmstudio/bin"
# End of LM Studio CLI section

```

# Winboat

## prerequisites
```shell

sudo pacman -Syu nvm
. /usr/share/nvm/init-nvm.sh

nvm install latest        # download latest node, e.g. 25.2.1
nvm use 25.2.1            # enable node version
nvm aloas default 25.2.1  # set node version as default

yay -S winboat
```

