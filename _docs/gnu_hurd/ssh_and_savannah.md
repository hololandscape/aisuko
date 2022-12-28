---
title       : "ssh and savannah"
excerpt     : "ssh and savannah"
sitemap     : false
permalink   : /docs/ssh_savannah/
toc         : true
---


## Why we need ssh key here?

It is for version control repository access. And SSH access is allowed for registered memebers who are a member of at least on project. 


## Upgrading ssh user key access to ED25519 keys.


ED25519 keys were introduced in OpenSSH 6.5 and offers better security with faster performance using a more compact key. Using the ED 25519 user key also enables using the ED25519 host key at the same time.

```
ssh-keygen -t ed25519
```

## Upgrading the new key to the savannah.gnu.org

Copying the contents of the resulting file ~/.ssh/id_ed25519.pub into the form at https://savannah.gnu.org/my/admin/editsshkeys.php


We need to confirm it will go well, so after upgrading new key please wait for an hour and try again because many tasks are implemented by hourly cron jobs.


## Testing ssh key is going to work

```
ssh -vvv yourlogin@cvs.savannah.gnu.org
```

If you get the following message, then things are working okay for you.

```
You tried to execute:
Sorry, you are not allowed to execute that command.
Connection to cvs.savannah.gnu.org closed.
```

Savannah server's security policy is implemented by fail2ban(six failures in one minutes bans your IP for ten minutes).


## Source:
[https://savannah.gnu.org/maintenance/SshAccess/](https://savannah.gnu.org/maintenance/SshAccess/)

