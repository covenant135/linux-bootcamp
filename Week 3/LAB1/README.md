# Lab 1: Install a LAMP stack on an Azure Linux VM

1. Create a resource group
2. Create a virtual machine
3. Open port 80 for web traffic
4. SSH into your VM
5. Install Apache, MySQL, and PHP
6. Install WordPress

### Notes:

Tutorial: Install a LAMP stack on an Azure Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-lamp-stack

Sample Gist
* https://gist.github.com/mikepfeiffer/96d659042f0575a617648a33c92b8f4a

Build and run a web application with the MEAN stack on an Azure Linux virtual machine
* https://docs.microsoft.com/en-us/learn/modules/build-a-web-app-with-mean-on-a-linux-vm/

MEAN Stack App
* https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm

 # Create a resource group
 az group create --name lampserver --location eastus

# Create a virtual machine
az vm create --resource-group lampserver --name olaweb --public-ip-sku --generate-ssh-keys -- --admin-username coven

# Open port 80 for web traffic

az vm open-port --port 80 --resource-group lampserver --name olaweb

# SSH into your VM
Using azure cli, i typed in


ssh coven@20.185.252.139 
and i was in

# Install Apache, MySQL, and PHP
using the line of code below, i got apache running via the public ip

sudo apt update && sudo apt install lamp-server 

i was then asked if i can continue and typed y

i verified apache installation using 

apache2 -v 
and open the public ip @  http://20.185.252.139/


tried verifying mysql installation using 
mysql -v
but was denied access and ask to set in password and other feature. To do this,  the following steps were taken, code

mysql_secure_installation

Afterwards, i was prompted for some security privileges and i set a new password (hint: basic digi)

i tested login to the mysql and i had to supply my password (hint: basic digi)
and i was let in
\h is help  \q is quit  \c is clear current input statement

Line of code to validate the php page 

sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'

# Install WordPress
This was done with:

sudo apt install wordpress -y

# Create WordPress DB Script
sudo nano wordpress.sql