VMWare Commands

```bash
vmware-hgfsclient # list shared directories
/usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other # mount all shares
vmhgfs-fuse .host:/my-shared-folder /shared -o allow_other -o uid=1000 # mount 'my-shared-folder' in guest-vm

# permanent mount -> add to /etc/fstab
vmhgfs-fuse     /mnt/hgfs   fuse    defaults,allow_other    0    0
vmhgfs-fuse     /mnt/hgfs   fuse    defaults,allow_other,uid=1000   0   0

```
