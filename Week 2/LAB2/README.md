# Lab 2: Manage Linux VMs with the AWS CLI

1. Create virtual machine
2. Connect to VM
3. Understand VM images
4. Understand VM sizes
5. VM power states
6. Management tasks

### Notes:

Quickstart: Create a Linux VM
* https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/

Using a custom Amazon machine image (AMI)
* https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.customenv.html

Quickstart: Restart VM via CLI
* https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html

Quickstart for AWS CloudShell
* https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html

# Lauching an INStance, A VM

I lauched both a linux instance and a windows intance. Unable to connect with the windows instance but connected succesfully with the linux instance. The instance image id were sought for using the aws service  instance search

aws ec2 run-instances --image-id ami-xxxxxxxx  --instance-type t2.micro --key-name olaaws --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e

# Connecting to an instance

There are several ways of conencting to the instance. This primary depends on the way kind of image used in the creation of the instance. For windows instance, we can use RDP or EC2 Instance connect. More so, if you have a linux instance, it can be connected to via SSH, EC2 instance connect.

using SSH connect, the following steps were used (NB: i deleted the instance after november 30.)

ssh -i /path/olaaws.pem ec2-user@public-dns-name

It then requires a confirmation push (yes).


# Install web server
The following line of code aided in installing the an apache server

sudo yum update -y
sudo yum install -y httpd
sudo service httpd start

we can close the ec2-user access afterwards and the server will still be running by using the code:

exit

 View the web server in action

 My lauched apache web had this piblic address

 http://18.207.158.41


# Tasks 3- 6 were diligently studied and monitored using the provided links
