# Installation and Configuration of Ansible Master Server

## Prerequisites:
```
Create EC2 Instance - (Ansible Administrative Server) (Amazon Linux 2 AMI (HVM), SSD Volume Type - ami-009d6802948d06e52 | t2.micro)
Create Security Group and open SSH, HTTP, and HTTPS ports.
Run commands as root (add sudo prefix for non-root)
```
### Install Ansible
```
yum update -y

#add EPEL (Extra Packages for Enterprise Linux)
 yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y

yum install Ansible -y

#check version
ansible --version
```
### Configure Users
```
useradd ansadmin
passwd ansadmin
```
### Configure SSH for EC2 Instances
```
vi /etc/ssh/sshd_config
