### replace string in file
    sed -i 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # linux
    sed -i '.original' -e 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # macOS (-i needs value to create backup file, in this example 'k3s-pi.kube.config.original')
    

## prepare, mount, unmount mass storage
### disk / storage infos
    sudo blkid # get UUID / PARTUUID

### partitioning
    sudo fdisk -l               # show disks and paritions
    sudo fdisk /dev/sda         # start partitioning
        # press 'g' -> new partition table with GPT
        # press 'n' -> new partition
        # press 'w' -> write and exit
        
    sudo mkfs.ext4 /dev/sda1    # format partition /dev/sda1 with ext4     
    
### mount / unmount
    sudo mkdir /media/usb; sudo chown myuser /media/usb    
    sudo mount /dev/sda1 /media/usb     # mount 
    sudo umount /media/usb              # unmount
    sudo mount -a                       # mount partitions from /etc/fstab

### benchmark write- / read-speed
    sync; time dd if=/dev/zero of=./test.tmp bs=500K count=1024; time sync
    dd if=./test.tmp of=/dev/null bs=500K count=1024
    rm ./test.tmp
