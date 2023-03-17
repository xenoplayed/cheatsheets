    loadkeys de-latin1

    timedatectl status
    timedatectl list-timezone
    timedatectl set-timezone Europe/Berlin

    mkfs.ext4 -L ROOT /dev/sda6
    mkfs.ext4 -L HOME /dev/sda7
    mkswap -L SWAP

    mount -L ROOT /mnt
    mount -L HOME --mkdir /mnt/home
    swapon -L SWAP
    
    cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
    
    pacman -Sy
    pacman -S pacman-contrib
    
    rankmirrors -n 10 /etc/pacman.d/mirrorlist.bak > /etc/pacman.d/mirrorlist
    
    pacstrap -i /mnt base base-devel linux linux-lts linux-headers linux-firmware intel-ucode amd-ucode sudo nano vim git neofetch networkmanager dhcpcd pulseaudio

    genfstab -U /mnt >> /mnt/etc/fstab
    
    arch-chroot /mnt
    
    echo HOSTNAME > /etc/hostname
    echo LANG=de_DE.UTF-8 > /etc/locale.conf
    nano /etc/locale.gen
    locale-gen
    
    echo KEYMAP=de-latin1 > /etc/vconsole.conf
    echo FONT=lat9w-16 >> /etc/vconsole.conf

    passwd
    
    usueradd -m xeno
    
    password xeno
    
    usermod -aG wheel,storage,power xeno
    
    EDITOR=nano visudo
    
      # %wheel ALL=(ALL:ALL) ALL      # uncomment this line
      # Defaults timestamp_timeout=0  # add this line
      
    nano /etc/hosts   # add following lines
    
      127.0.0.1       localhost
      ::1             localhost
      127.0.1.1       l2d2.localdomain        localhost
      
    ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
    hwclock --systohc
    
    mount /dev/sda2 /boot/efi
    
    pacman -S grub efibootmgr dosfstools mtools ntfs-3g
    
    reboot
    
    nano /etc/default/grub
    
      # GRUB_DISABLE_OS_PROBER=false # uncomment line
    
    pacman -S os-prober
    
    # https://wiki.archlinux.de/title/GRUB
    grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck
    grub-mkconfig -o /boot/grub/grub.cfg
    
    
    
    
