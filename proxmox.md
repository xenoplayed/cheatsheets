# cloud-init setup


```bash
## on Proxmox host
### download image
wget https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2

### if downloaded file is of type 'img' convert to 'qcow2'
mv ubuntu-22.04-server-cloudimg-amd64.img ubuntu-template.qcow2

### create vm
qm create 100 --name "centos8-cloudinit-template" --memory 2048 --net0 virtio,bridge=vmbr0

### resize image
qemu-img resize ubuntu-template.qcow2 20G

### import image into proxmox storage 'local-lvm'
qm importdisk 100 CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2 local-lvm

### attach disk to vm
qm set 100 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-100-disk-0

### change boot order
qm set 100 --boot c --bootdisk scsi0

### add cloudinit drive
qm set 100 --ide2 local-lvm:cloudinit

### add serial console
qm set 100 --serial0 socket --vga serial0

qm clone 100 101 --name test-box
qm set 101 --sshkey ~/.ssh/id_rsa.pub
qm set 101 --ipconfig0 ip=192.168.0.100/24,gw=192.168.0.1
qm start 101


## in VM

# update & install qemu-guest-agent
sudo apt update && sudo apt upgrade && sudo apt install qemu-guest-agent
# enable service
sudo systemctl enable qemu-guest-agent

# reset machine id and delete cloudinit artifacts
sudo truncate -s 0 /etc/machine-id /var/lib/dbus/machine-id
sudo cloud-init clean

# poweroff
sudo shutdown -h now

## on Proxmox host

# convert into template
qm template 100

pveum role add TFUser -privs \
    "VM.Allocate VM.Clone \
    VM.Config.CDROM VM.Config.CPU \
    VM.Config.Cloudinit VM.Config.Disk \
    VM.Config.HWType VM.Config.Memory \
    VM.Config.Network VM.Config.Options \
    VM.Monitor VM.Audit VM.PowerMgmt \
    Datastore.AllocateSpace \
    Datastore.Audit"

pveum user add terraform@pve
pveum aclmod / -user terraform@pve -role TFUser
pveum user token add terraform@pve terraform-token --privsep=0

## other example
# TODO: add commands to install qemu-guest-agent in cloud-init image

# create vm
sudo qm create 9000 --name "ubuntu-2204-cloudinit-template" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0

# import iso image
sudo qm importdisk 9000 ubuntu-22.04-minimal-cloudimg-amd64.img DataStorage

#
sudo qm set 9000 --scsihw virtio-scsi-pci --scsi0 DataStorage:vm-9000-disk-0
sudo qm set 9000 --boot c --bootdisk scsi0
sudo qm set 9000 --ide2 DataStorage:cloudinit
sudo qm set 9000 --serial0 socket --vga serial0
sudo qm set 9000 --agent enabled=1

sudo qm template 9000

sudo qm clone 9000 999 --name test-clone-cloud-init

sudo qm set 999 --sshkey ~/.ssh/id_rsa.pub

sudo qm set 999 --ipconfig0 ip=192.168.177.199/24,gw=192.168.178.1

sudo qm start 999

ssh ubuntu@10.98.1.96
```
