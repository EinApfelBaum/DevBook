---
created: 22.10.2021
tags: linux shell fish
parent: Linux
---

# Extend fish PATH

`$PATH` is an environment variable containing the directories that fish searches for commands. Unlike other shells, `$PATH` is a list, not a colon-delimited string.

To prepend `/usr/local/bin` and `/usr/sbin` to `$PATH`, you can write:

```bash
set PATH /usr/local/bin /usr/sbin $PATH
```

To remove `/usr/local/bin` from `$PATH`, you can write:

```bash
set PATH (string match -v /usr/local/bin $PATH)
```

For compatibility with other shells and external commands, `$PATH` is a path variable, and so will be joined with colons (not spaces) when you quote it:

```bash
echo "$PATH"
/usr/local/sbin:/usr/local/bin:/usr/bin
```

and it will be exported like that, and when fish starts it splits the `$PATH` it receives into a list on colon.

You can do so directly in `config.fish`, like you might do in other shells with `.profile`. See [this example](https://fishshell.com/docs/current/tutorial.html#path-example):

A faster way is to modify the `$fish_user_paths` universal variable, which is automatically prepended to `$PATH`. For example, to permanently add `/usr/local/bin` to your `$PATH`, you could write:

```bash
set -U fish_user_paths /usr/local/bin $fish_user_paths
```

The advantage is that you don't have to go mucking around in files: just run this once at the command line, and it will affect the current session and all future instances too. (Note: you should NOT add this line to `config.fish`. If you do, the variable will get longer each time you run fish!)

---

## Resources

* [https://github.com/fish-shell/fish-shell](https://github.com/fish-shell/fish-shell)
* [https://fishshell.com/docs/current/tutorial.html#tut-lists](https://fishshell.com/docs/current/tutorial.html#tut-lists)
* [https://fishshell.com/docs/current/index.html#variables-path]([https://link](https://fishshell.com/docs/current/index.html#variables-path))
* [https://fishshell.com/docs/current/tutorial.html#tut-universal](https://fishshell.com/docs/current/tutorial.html#tut-universal)
