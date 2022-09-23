# Getting started
## Logging into the server
At the moment the server is only accessible via SSH, and only certain users have been given an account.  This is planned to change in the future though.

To log in use the following command

```
ssh username@netsoc.com
```

You will then be asked for your password.  After entering it, you will be logged in at your home directory. Feel free to create new files here, this is your space!

## Setting up ssh keys
You can set up an ssh key pair, so you will not be asked for your password every time you login.

1. Create the key pair (you will be given the option to enter a passphrase. This passphrase deals with how the key pair is stored, so if you enter a passphrase you will have to enter it every time you try to log into the server)
```
ssh-keygen -t rsa
```
2. Copy the public key to the server
```
ssh-copy-id -i ~/.ssh/id_rsa.pub username@netsoc.com
```

You can now login without having to enter your password.
