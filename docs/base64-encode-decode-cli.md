---
created: 14.07.2021
tags: encryption cli linux
---

# Encode and decode base64

```bash
# base64 encoded
echo -n 'input' | openssl base64
# => aW5wdXQ=

# base64 decode
echo 'aW5wdXQ=' | base64 --decode
# => input
```
