# Lab 2: Manage Linux VMs with the Azure CLI

1. Create resource group
2. Create virtual machine
3. Connect to VM
4. Understand VM images
5. Understand VM sizes
6. VM power states
7. Management tasks

### Notes:

Quickstart: Create a Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

additonal resource
https://azure.microsoft.com/en-in/blog/vm-image-blog-post/


# Create a resource group

Using Azure CLI


Using the code below code, I created an azure resource group

az vm create --resource-group OLAARG  --location eastus


# Create virtual machine
az vm create --resource-group OLAARG --name OLAVMM --image UbuntuLTS --generate-ssh-keys
--admin-username cove --public-ip-sku Standard

# Connect to VM

To connect to my VM, i simply use the ssh command as describe below



ssh cove@201.116.16.32

after which I was requested to grant access and I did by typing in yes.

#  Understand VM images

Images are essential in the creation of VM. Several images are eavailable in azure for use and we can create ours. To know the available images, we code

az vm image list --output table

It can be streamlined to specific by:

az vm image list --offer WindowServer --all --output table

#  Understand VM sizes

Several sizes are available with  general purpose VM such as B, Dsv3, Dv3, DSv2, Dv2, Av2, D but commonly used is DsV2
others include Fsv2, Esv3, Ev3, M, DSv2, Dv2, Lsv2, Ls.

# VM power states
The state of the VM. It is always output when we launch a VM and we can also code the following lines to get the state:

az vm get-instance-view     --name OLAVMM  --resource-group OLAARG--query instanceView.statuses[1] --output table

# Management tasks

During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine. Additionally, you may want to create scripts to automate repetitive or complex tasks. Using the Azure CLI, many common management tasks can be run from the command line or in scripts. (as understood from the tutorials provided)