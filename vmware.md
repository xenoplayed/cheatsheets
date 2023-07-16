VMWare Commands

```bash
vmware-hgfsclient # list shared directories
vmhgfs-fuse .host:/my-shared-folder /shared -o allow_other -o uid=1000 # mount 'my-shared-folder' in guest-vm
```
