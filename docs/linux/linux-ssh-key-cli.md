---
created: 22.10.2021
tags: linux ssh cli
parent: Linux
---

# ssh cli

```bash
# Generating public/private rsa key pair.
ssh-keygen -b 4096

# Copy public key to remote
ssh-copy-id -i .ssh/key_rsa.pub <USER>@<REMOTE IP>

ssh <USER>@<REMOTE IP>
```
