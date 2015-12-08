Introduction
============
SSH keys allow secure access between two computers.

Single Account
==============
If you have a single account with bitbucket or github, find the id_rsa.pub file in the ~ directory.

```bash
ls -al ~/.ssh
```

If there is no existing key, one may be created as follows :

```bash
ssh-keygen -t rsa -f ~/.ssh/id_rsa -N '' -C ''
```

Copy the public key to the clipboard and paste into bitbucket or github.

```bash
clip < ~/.ssh/id_rsa.pub
```

Multiple Accounts
=================
When using multiple accounts (logins) for bitbucket or github, multiple identity files (private keys) will need to 
be used.  In ~/.ssh directory, a private key should be generated and a config file created/updated.

Keygen
------
Generate a key with no passphrase:

```bash
ssh-keygen -t rsa -f ~/.ssh/{login} -N '' -C ''
```

This will create two files, {login} and {login}.pub.  The {login}.pub file will be needed for 
[bitbucket](../bitbucket) or [github](../github) configuration.

Config
------
Add/modify a [config](config) file to declare the {login} ssh host and map it to bitbucket.org with the
proper credentials.  This file, named "config", should be placed in ~/.ssh.

Usage
-----
When cloning, use the {login} as the host name. 


References
==========
[github ssh](https://help.github.com/articles/generating-ssh-keys/)
