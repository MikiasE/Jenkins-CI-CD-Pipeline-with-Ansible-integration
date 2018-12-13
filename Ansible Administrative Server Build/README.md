# Installation and Configuration of Ansible Administrative Server

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

#provide sudo access (scroll to the bottom and add under "#includedir /etc/sudoers.d")
visudo
"ansadmin ALL=(ALL) NOPASSWD: ALL"
```
### Configure SSH
```
vi /etc/ssh/sshd_config

#disable "PasswordAuthentication no" and enable "PasswordAuthentication yes"

service sshd restart

#create ssh key
ssh-keygen
cd .ssh/

#transfer ssh key to ansible client based on private IP
ssh-copy-id [your client private IP]
yes

#test ssh success
ssh [your client private IP]
exit
```
### Configure Ansible Playbook
```
#configure hosts
sudo vi /etc/ansible/hosts

#add at the bottom:
[all_hosts]
[*insert your client private IP*]

#test copy
cd ~
cat > test.html # (<h1> Testing, Testing, 1.2.3 </h1>)
ansible all -m copy -a "src=/home/ansadmin/test.html dest=/home/ansadmin"

```
