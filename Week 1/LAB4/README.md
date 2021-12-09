# Lab 4: Create and use an SSH public-private key pair for Linux VMs in Azure

1. Supported SSH key formats
2. Create an SSH key pair
3. Provide an SSH public key when deploying a VM
4. SSH into your VM

### Notes:

Quickstart: SSH for Linux VMs
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart


#  Supported SSH key formats
The supported SSK Key formats in Azure include 
RSA (public-private key)


# Create an SSH key pair

az sshkey create --name "olassh" --resource-group "OLAARG"


# Provide an SSH public key when deploying a VM

az vm create --resource-group OLAARG --name OLAVMMM --image UbuntuLTS  --ssh-key-value ~/.ssh/1639023231_6917665.pub --admin-username cove --size Standard_DS2_V2 --data-disk-sizes-gb 128  --public-ip-sku Standard

# SSH into your VM
 ssh -i ~/.ssh/1639023231_6917665.pub cove@20.102.30.127
