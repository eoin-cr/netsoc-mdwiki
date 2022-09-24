# Getting started
## How to read commands
If you're new to reading linux terminal tutorials, the `$` and `#` shown before commands in this documentation may be new to you.  The `$` simply represents a command run by a regular user (i.e. not root) in the terminal, and `#` represents a command run by the root user in the terminal.  *Do not include the `$` or `#` in the command when you're running it*.

## Logging into the server
At the moment the server is only accessible via SSH, and only certain users have been given an account.  This is planned to change in the future though.

To log in use the following command

```
$ ssh username@netsoc.com
```

You will then be asked for your password.  After entering it, you will be logged in at your home directory. Feel free to create new files here, this is your space!

## Setting up ssh keys
You can set up an ssh key pair, so you will not be asked for your password every time you login.

1. Create the key pair (you will be given the option to enter a passphrase. This passphrase deals with how the key pair is stored, so if you enter a passphrase you will have to enter it every time you try to log into the server in order to unencrypt your ssh private key (the passphrase does not have to be the same as the password to your account on the server))
```
$ ssh-keygen -t rsa
```
2. Copy the public key to the server
```
$ ssh-copy-id -i ~/.ssh/id_rsa.pub username@netsoc.com
```

You can now login without having to enter your password.

## Setting up a shell alias
You can set up an alias, which means you can simply type `netsoc` or the like, instead of having to type `ssh user@netsoc.com`.

Firstly you'll want to check which shell you're using by running `which $SHELL`. It will probably be `/bin/bash` although it may be another one.  Check online to see where the config file for the the shell is if you're using a different one.

For bash run
```
$ nano ~/.bashrc
```
and then enter
```
alias netsoc='ssh user@netsoc.com'
```
(Note that the name does not have to be netsoc, it can be anything you want, just make sure it isn't already a command!)
Then run
```
$ source ~/.bashrc
```
and the alias will be applied.  Now you can just type `netsoc` to log in!
