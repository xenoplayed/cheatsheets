### replace string in file

    sed -i 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # linux
    sed -i '.original' -e 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # macOS (-i needs value to create backup file, in this example 'k3s-pi.kube.config.original')

## prepare, mount, unmount mass storage

### disk / storage infos

    sudo blkid # get UUID / PARTUUID

### memory

    free        # Display amount of free and used memory in the system

### partitioning

    sudo fdisk -l               # show disks and paritions
    sudo fdisk /dev/sda         # start partitioning
        # press 'g' -> new partition table with GPT
        # press 'n' -> new partition
        # press 'w' -> write and exit
        
    sudo mkfs.ext4 /dev/sda1    # format partition /dev/sda1 with ext4     

### mount / unmount

    sudo mkdir /media/usb; sudo chown $USER:$USER /media/usb; ls -lah /media     # chown needed before mounting, to allow write access to $USER
    sudo mount /dev/sda1 /media/usb     # mount
    sudo mount /dev/sda1 /media/usb -o uid=pi,gid=pi
    sudo umount /media/usb              # unmount
    sudo mount -a                       # mount partitions from /etc/fstab

### benchmark write- / read-speed

    sync; time dd if=/dev/zero of=./test.tmp bs=500K count=1024; time sync
    dd if=./test.tmp of=/dev/null bs=500K count=1024
    rm ./test.tmp

# services

    systemctl list-units [PATTERN]      # list units [matching pattern]
    systemctl list-timers [PATTERN]     # list timers [matching pattern]
    systemctl list-sockets [PATTERN]    # list sockets [matching pattern]
    systemctl start UNITNAME
    systemctl stop UNITNAME
    systemctl restart UNITNAME
    systemctl status UNITNAME

# networking

    ip addr         # interface config
    ip route        # routing config
    netstat -nr     # don't resolve names, kernel ip routing table
    netstat -ntlp   # don't resolve names, only tcp sockets, list, display programe name for sockets

# others

```bash
# systemctl
systemctl list-units|list-timers|list-sockets
systemctl start|stop|restart|reload UNIT...
systemctl is-active|is-enabled UNIT...
systemctl status UNIT...
systemctl enable|disable UNIT...

# journalctl
journalctl -u home.mount -u networking.service # multiple units at once
journalctl -f -u apache # live watch
journalctl --since "2016-07-01" --until "2 minutes ago" # filter by date
journalctl -p err -b # filter by label error, warning, alert or emergency

# other useful commands
export PATH=$PATH:~/opt/bin     # add environment variable to path
which ls                        # show path to linux command
truncate -s 5M ostechnix.txt    # Create files of a certain size
fallocate -l 450M file.dat      # Preallocate space to, or deallocate space from a file.

find -maxdepth 1 -type d -exec du -h -d 0 {} \; # used dir space
```

https://www.baeldung.com/linux/list-by-size