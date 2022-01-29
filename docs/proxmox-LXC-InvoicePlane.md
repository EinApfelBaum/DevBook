---
created: 17.10.2021
tags: proxmox cli InvoicePlane
---

# install InvoicePlane in LXC

```bash

# after installing apache2 webserver

apt-get install unzip
apt-get install libapache2-mod-php7.3
apt-get install php7.3-mysql php7.3-json php7.3-mbstring php7.3-recode php7.3-xmlrpc 

cd var/www/html

wget https://www.invoiceplane.org/download/v1.5.11

unzip v1.5.11

chown -R www-data:www-data /var/www/html/

# make a copy of the ipconfig.php.example file and rename the copy to ipconfig.php
# Open the ipconfig.php file and add your URL in it like described in the file.
# --> url=http://myDomain.de

# To get remote write access with VSCode, a new user must be created to access it with SSH. User must be in the www-data group. 
# Folders and files must additionally get g+w rights

# with root
chown -R "User":www-data /var/www/html/

# Adjust folder rights
find -type -d -exec chmod g+w {} \;

```
