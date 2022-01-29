---
created: 17.10.2021
tags: proxmox cli
---

# Commands for new Linux container

```bash
# with root user

# first update and upgrade
apt-get update | apt-get upgrade


# install fish
apt-get install fish -y

# make fish the default shell for root
chsh -s /usr/bin/fish

# ectend PATH environment 
set -U fish_user_paths /usr/local/bin $fish_user_paths


# install apache webserver, if needed
apt-get install apache2 -y

# install htop
apt-get install htop -y


########################
# maybe for ssh access
# add user with home 
useradd --create-home *Username*

# add password for user
passwd *Username*

# change shell of the user
chsh -s /usr/bin/fish *Username*

# ssh key must be created on client side (laptop/workstation)
# 1. create ssh key with ui program 
# 2. create ssh key with terminal
ssh-keygen -b 4096 -f *filename*

# after you create the ssh key
# copy public key to remote server
ssh-copy-id -i .ssh/*filename*.pub -o IdentitiesOnly=yes *Username*@*ServerIP*
  ```
