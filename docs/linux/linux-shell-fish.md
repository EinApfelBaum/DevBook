---
created: 22.10.2021
tags: linux fish shell server
parent: Linux
---

# Switching to fish

If you wish to use fish as your default shell, use the following command:

```bash
chsh -s /usr/local/bin/fish
```

`chsh` will prompt you for your password and change your default shell. (Substitute /usr/local/bin/fish with whatever path fish was installed to, if it differs.) 
Log out, then log in again for the changes to take effect.

Use the following command if fish isn’t already added to /etc/shells to permit fish to be your login shell:

```bash
echo /usr/local/bin/fish | sudo tee -a /etc/shells
```

To switch your default shell back, you can run `chsh -s /bin/bash` (substituting /bin/bash with /bin/tcsh or /bin/zsh as appropriate).

---

## Resources

* [https://github.com/fish-shell/fish-shell](https://github.com/fish-shell/fish-shell)
