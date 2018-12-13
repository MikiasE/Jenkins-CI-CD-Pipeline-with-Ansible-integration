# Installation and Configuration of Ansible Slave Server

## Prerequisites:
```
Create EC2 Instance - (Ansible Administrative Server) (Amazon Linux 2 AMI (HVM), SSD Volume Type - ami-009d6802948d06e52 | t2.micro)
Create Security Group and open SSH, HTTP, and HTTPS ports.
Run commands as root (add sudo prefix for non-root)
```
### Install Ansible
```
yum update -y

#add EPEL (Extra Packages for Enterprise Linux) to get ansible package
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y

yum install Ansible -y

#check version
ansible --version
```
### Configure Users
```
useradd ansadmin
passwd ansadmin

#provide sudo access (scroll to "Allow root to run any commands anwhere" and add below)
visudo
"ansadmin ALL=(ALL) NOPASSWD: ALL"
```
### Configure SSH for EC2 Instances
```
vi /etc/ssh/sshd_config

#disable "PasswordAuthentication no" and enable "PasswordAuthentication yes"

service sshd restart
```
