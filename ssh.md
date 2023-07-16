Linux
```bash
ssh-keygen -t ed25519 -C "me@localhost" -f ~/.ssh/test_key  # create keypair with eliptic curve
ssh-keygen -t rsa -N '' -f ubuntu_rsa <<< y 2>&1 >/dev/null

ssh-add -l                                                  # list loaded identities
ssh-add -D                                                  # remove all identities from agent
```

    

Windows 10 (powershell)
```powershell
echo y | ssh-keygen.exe -t rsa -N '""' -f ubuntu_rsa | Out-Null
```