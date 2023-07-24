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

```

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

