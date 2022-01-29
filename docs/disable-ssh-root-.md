---
created: 17.10.2021
tags: linux ssh
---

# Disable ssh root login

If you want to prohibit direct SSH root login under Debian, you need at least one other user besides the root user who is allowed to log in to the server. With this user you then switch to the root account.

> ATTENTION: If you have not created another user, you lock yourself out of the system!

## PermitRootLogin no

Edit the file `/etc/ssh/sshd_config and set`

```config
PermitRootLogin yes
```

to

```config
PermitRootLogin no
```

Then restart the SSH service

`/etc/init.d/ssh restart (alternatively: service ssh restart)`

Now user root is no longer allowed to log in directly to the system. You log in normally with a user and then switch with `su` to the root account.

## AllowGroups

With the AllowGroups parameter you can additionally limit which users are allowed to log in via SSH.

Excerpt from `man sshd_config`:

> AllowGroups
>
> This keyword can be followed by a list of group name patterns, separated by spaces. If specified, login is allowed only for users whose primary group  or supplementary group list matches one of the patterns. Only group names are valid; a numerical group ID is not recognized. By default, login is  allowed for all groups. The allow/deny directives are processed in the following order: DenyUsers, AllowUsers, DenyGroups, and finally AllowGroups.
>
> To create a group named `sshusers` and add a user to this group, run the following commands as the root user:
>
> `addgroup --system sshusers`
> `adduser xyz sshusers`

Then configure the following options in `/etc/ssh/sshd_config`:

```config
LoginGraceTime 30
AllowGroups sshusers
PermitRootLogin no
StrictModes yes
```

Then restart the SSH service: `/etc/init.d/ssh restart`
