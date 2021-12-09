# Lab 1: Create a Linux virtual machine with the AWS CLI

1. Launch AWS Cloud Shell
3. Create virtual machine
4. Open port 80 for web traffic
5. Connect to virtual machine
6. Install web server
7. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/

Quickstart for AWS CloudShell
* https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html

# Task 1: Launching AWS CLoud Shell

Just by getting an AWS account created and loggin in, the cloud shell access is just close by the seach tab with -> symbol

# Task 2  Create a Virtual Machine

To create a VM in AWS, you need a working VPC.

The following Link of Code helps to get the VPC Running and then Lauching a AWS EC2 instance (VM)

# Create A VPC

aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text

prints    vpc-********

# Create a Subnet
aws ec2 create-subnet --vpc-id vpc-********** --cidr-block 10.0.1.0/24
aws ec2 create-subnet --vpc-id vpc-******** --cidr-block 10.0.0.0/24

# Make your subnet public
After you've created the VPC and subnets, you can make one of the subnets a public subnet by attaching an internet gateway to your VPC, creating a custom route table, and configuring routing for the subnet to the internet gateway.

we begin with an internet gateway (igw)

aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
prints  igw-******
Attach the igw to your vpc
aws ec2 attach-internet-gateway --vpc-id vpc-****** --internet-gateway-id igw-**********

Create a route-table 

aws ec2 create-route-table --vpc-id vpc-***** --query RouteTable.RouteTableId --output text

prints rtb-*******

Create a route in the route table that points all traffic (0.0.0.0/0) to the internet gateway using the following create-route command.

aws ec2 create-route --route-table-id rtb-******** --destination-cidr-block 0.0.0.0/0 --gateway-id igw-*****

To confirm that your route has been created and is active, you can describe the route table using the following describe-route-tables command.

aws ec2 describe-route-tables --route-table-id rtb-**********

Then associate the route table to a subnet 

aws ec2 associate-route-table  --subnet-id subnet-**** --route-table-id rtb-********

its good to modify the behaviour of public IP, by default, Aws will not associate a public ip to any instance lauched into the subnet but by using the code below, we can just do that or use the portal to permit public ip lauch on every instance into the subnet

aws ec2 modify-subnet-attribute --subnet-id subnet-********* --map-public-ip-on-launch

Create a key pair to use for your instance, download and keep safe
aws ec2 create-key-pair --key-name ***** --query 'KeyMaterial' --output text > **********.pem

aws ec2 describe-key-pairs --key-name MyKeyPair

you can delete key pair by aws ec2 delete-key-pair --key-name *****

# Create Security Group

SG  essentially operates as a firewall, with rules that determine what network traffic can enter and leave. 

aws ec2 create-security-group --group-name my-sg --description "My security group" --vpc-id vpc-1a2b3c4d

The following example shows how to add a rule for RDP (TCP port 3389) to an EC2-VPC security group with the ID sg-903004f8 using your IP address.
To start, find your IP address.
curl https://checkip.amazonaws.com

when you get it, add it to the SG

aws ec2 authorize-security-group-ingress --group-id sg-903004f8 --protocol tcp --port 3389 --cidr UR IP

To enable SSH, use
aws ec2 authorize-security-group-ingress --group-id sg-****** --protocol tcp --port 22 --cidr UR ip or general 0.0.0.0/0

aws ec2 authorize-security-group-ingress --group-id sg-****** --protocol tcp --port 80 --cidr 0.0.0.0/0

# Lauching an INStance, A VM

I lauched both a linux instance and a windows intance. Unable to connect with the windows instance but connected succesfully with the linux instance. The instance image id were sought for using the aws service  instance search

aws ec2 run-instances --image-id ami-xxxxxxxx  --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e

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

we can close the ec2-user access afterwards and the server will still be running

exit

 View the web server in action

 My lauched apache web had this piblic address

 http://18.207.158.41

