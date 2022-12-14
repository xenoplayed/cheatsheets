
  ssh-add -D # remove all identities from agent

  ssh-keygen -t ed25519 -C "me@localhost" -f ~/.ssh/test_key # create keypair with eliptic curve
