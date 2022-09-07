---
title       : "ssh and savannah"
excerpt     : "ssh and savannah"
sitemap     : false
permalink   : /docs/ssh-savannah/
toc         : true
---

# Upgrading ssh user key access to ED25519 keys.


ED25519 keys were introduced in OpenSSH 6.5 and offers better security with faster performance using a more compact key. Using the ED 25519 user key also enables using the ED25519 host key at the same time.

```
ssh-keygen -t ed25519
```

