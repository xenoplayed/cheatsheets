Linux
```bash
ssh-keygen -t ed25519 -C "me@localhost" -f ~/.ssh/test_key  # create keypair with eliptic curve
ssh-keygen -t rsa -N '' -f ubuntu_rsa <<< y 2>&1 >/dev/null

ssh-copy-id -i ~/.ssh/id_rsa.pub user@server                        # copy pub key to server
cat id_rsa.pub | ssh user@server 'cat>> ~/.ssh/authorized_keys'     # alternative to ssh-copy-id

ssh-add -l                                                  # list loaded identities
ssh-add -D                                                  # remove all identities from agent
```

    

Windows 10 (powershell)
```powershell
echo y | ssh-keygen.exe -t rsa -N '""' -f ubuntu_rsa | Out-Null
```
