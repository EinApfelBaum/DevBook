---
created: 17.08.2021
tags: git submodule cli
---

# Remove a submodule

```bash
git submodule deinit <path_to_submodule>
git rm <path_to_submodule>
git commit -m "Removed submodule "
rm -rf .git/modules/<path_to_submodule>
```

---

## Resources

* [https://gist.github.com/myusuf3/7f645819ded92bda6677](https://gist.github.com/myusuf3/7f645819ded92bda6677)
