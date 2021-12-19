# Lab 2: Install a LAMP stack on an Azure Linux VM

1. Prepare the LAMP server
2. Test your Lamp server
3. Secure the database server
4. (Optional) Install phpMyAdmin

### Notes:

Tutorial: Install a LAMP web server on the Amazon Linux AMI
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html

Tutorial: Host a WordPress blog on Amazon Linux 2
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hosting-wordpress.html

Sample Gist
* https://gist.github.com/mikepfeiffer/c079608703e604224e58a3d40d0fa043#file-lamp-linux-aws-sh


# Prepare lamp Server

#An instance is needed here and it must be in a running state before we can install a LAMp (linux APache2 MYSQl PHP) server

aws ec2 run-instances --image-id ami-xxxxxxxx  --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e

#the ami used was ami-0ed9277fb7eb570c9

#i connected to the instance using ec2 instance (a webpage connect option) 

#The instance needed for basic update,

sudo yum update -y

#to install the lamp server
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

#or to install apache only
sudo yum install -y httpd mariadb-server

#to start the apache server

sudo systemctl   start httpd

#my public ip was 
44.192.46.98
#public dns
ec2-44-192-46-98.compute-1.amazonaws.com
#to enable instance lauch plus apache start

sudo systemctl enable httpd

to check if it is running

sudo systemctl is-enabled httpd

#chane group ownership 
sudo chown -R ec2-user:apache /var/www

#To add group write permission
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;

find /var/www -type f -exec sudo chmod 0664 {} \;


# TEst  LAMP server

#create php file in apache document root
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php



# Secure Database

sudo systemctl start mariadb

sudo mysql_secure_installation

#was prompted for a password and I set a new password as default had no password



# 

sudo yum install php-mbstring php-xml -y





