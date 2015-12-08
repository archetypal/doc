Introduction
============
SSH keys allow secure access between two computers.

Single Account
==============
If you will only have a single account with bitbucket or github, find the id_rsa.pub file in the ~ directory.

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
When multiple accounts are used on bitbucket or github, multiple SSH keys are needed, one to identify each account.
Therefore, multiple identity files (private keys) will need to be used.  In ~/.ssh directory, a private key
should be generated and a config file created/updated to map the identity file to host.

Keygen
------
Generate a key with no passphrase (-C '{login}' may be omitted if the public key should not be commented):

```bash
ssh-keygen -t rsa -f ~/.ssh/archetypal -N '' -C 'archetypal'
```

Copy the public key and paste into [bitbucket](../bitbucket) or [github](../github) configuration.

```bash
clip < ~/.ssh/archetypal.pub
```

Config File
-----------
Add/modify a [config](config) file to declare the {login} ssh host and map it to bitbucket.org with the
proper credentials.  This file, named "config", should be placed in ~/.ssh.

```bash
cp config ~/.ssh/
```

Or, create a config file in ~/.ssh with the following contents.

```
Host at
 HostName github.com
 IdentityFile ~/.ssh/archetypal
```

Usage
-----
When cloning, use git@at as the host name.  For example, if cloning this repository:

```bash
git clone git@at:archetypal/doc.git
```


References
==========
[github ssh](https://help.github.com/articles/generating-ssh-keys/)
