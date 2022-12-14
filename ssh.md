    ssh-keygen -t ed25519 -C "me@localhost" -f ~/.ssh/test_key  # create keypair with eliptic curve
    ssh-add -l                                                  # list loaded identities
    ssh-add -D                                                  # remove all identities from agent
