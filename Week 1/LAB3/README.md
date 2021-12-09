# Lab 3: Manage Azure disks with the Azure CLI

1. Default Azure disks
2. Azure data disks
3. VM disk types
4. Launch Azure Cloud Shell
5. Create and attach disks
6. Prepare data disks
7. Take a disk snapshot

### Notes:

Quickstart: Manage Azure disks
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart


# lauch Azure Cloud Shell

# Create and Attach Disk
Disk can be created at resource group creation or we can create and attach it to an existing VM

For the former: 
az vm create  --resource-group OLAARG  --name OLAVM   --image UbuntuLTS   --size Standard_DS2_v2   --admin-username azureuserv --public-ip-sku Standard --generate-ssh-keys   --data-disk-sizes-gb 128 128

az vm disk attach   --resource-group OLAARG    --vm-name OLAVMM   --name myDataDisk    --size-gb 128     --sku Premium_LRS     --new

# Prepare data disks
This task is aimed at configuring the disk for usage by the operating system. 
To do this, the following code we ran using the SSH commands

ssh azureuserv@20.106.132.110

sudo parted /dev/sdc --script mklabel gpt mkpart xfspart xfs 0% 100%
sudo mkfs.xfs /dev/sdc1
sudo partprobe /dev/sdc1
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
df -h | grep -i "sd"
sudo -i blkid

exit




# Take a disk snapshot

To DO this, we create a disk snapshot first

osdiskid=$(z vm show   -g OLAARG    -n OLAVM    --query "storageProfile.osDisk.managedDisk.id"  -o tsv)


   az snapshot create     --resource-group OLAARG     --source "$osdiskid"     --name osDisk-backup