# Lab 1: Create a Linux virtual machine with the Azure CLI

1. Launch Azure Cloud Shell
2. Create a resource group
3. Create virtual machine
4. Open port 80 for web traffic
5. Connect to virtual machine
6. Install web server
7. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

# Working in Laboratory 1
q
# Task 1: Lauch Azure Cloud Shell

To get this done, I simply signed in to my microsoft azure account/portal. Afterwards, I clicked >_ symbol to run the cloud shell. It prompted me to create an online storage and after which it launch display just a dollar sign.

# Task 2. Create a resource group

Using the code below code, I created an azure resource group

az vm create --resource-group olalab_2 --location eastus

# Task 3: Creating  day2 virtual machine

To create a virtual machine in my resource group, i dial in the fllowing line of code

az vm create --resource-group olalab_2 --name day2 --image UbuntuLTS --generate-ssh-keys
--admin-username covenant --admin-password WinePress$$$$ --public-ip-sku Standard


# Task 4: Opening port 80

az vm open-port --port 80 --resource-group olalab_2 --name day2



# task 5: Connecting to VM

To connect to my VM, i simply use the ssh command as describe below

ssh 20.116.16.32 
or if i had supplied a admin-username earlier I will type 

ssh username@201.116.16.32

after which I was requested to grant access and I did by typing in yes.

# Task 6: Installing a webserver

There are differnt webservers that can be install on ubuntults which include apache (very old), nginx, apche2 etc. To install the webserver, we code using sudo as follow 

sudo apt-get -y update 
sudo apt-get -y install webserver (apache2 or nginx)

# Reference
Learnt about az vm commands via

https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az_vm_create