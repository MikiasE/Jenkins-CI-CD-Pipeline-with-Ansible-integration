# Jenkins-CI-CD-Pipeline-with-Ansible-integration

Included Technologies: Apache2, Git, Maven, Jenkins, Tomcat

Languages: HTML, Java

This project demonstrates the process to configure a Jenkins continuous integration server on Amazon EC2. Once configured, Jenkins will be set up to build a Java projet with Maven, pulling the project from GitHub automatically, each time a change is pushed to a GitHub repository. Build will occur in Jenkins and the Deployment process will occur in Ansible. Ansible can be used to handle more complex pipeline build requirements. This project is a continuation of the ["Jenkins-CI-CD-Pipeline-Maven"](https://github.com/MikiasE/Jenkins-CI-CD-Pipeline-Maven)project.

Project walkthrough can be found here: http://www.mikiasemanuel.com/jenkins-ci-cd-pipeline-with-ansible-integration/

## Prerequisites:

Configure Ansible Administrative Server and Host.

Ansible Administrative (Master) Server Build is outlined [here](https://github.com/MikiasE/Jenkins-CI-CD-Pipeline-with-Ansible-integration/blob/master/Ansible%20Administrative%20Server%20Build/README.md).

Ansible Host (Slave) Server Build is outlined [here](https://github.com/MikiasE/Jenkins-CI-CD-Pipeline-with-Ansible-integration/tree/master/Ansible%20Slave%20Server%20Build/README.md).

*In this instance, the Tomcat Web Server will act as the Ansible Slave.*

Install "publish over ssh" Jenkins plugin.

### Create Jenkins playbook
```
mkdir ~/opt/playbooks/
mkdir ~/opt/playbooks/webapp/
mkdir ~/opt/playbooks/webapp/target/
cd /opt/playbooks/
cat copyfile.yml

#in copyfile.yml (added Tomcat IP to webserver host in /etc/ansible/hosts)
---
- hosts: web-servers
  become: true
  tasks:
    - name: copy war to tomcat server
      copy: 
        src: /opt/playbooks/webapp/webapp.war #will copy from ansible server to tomcat server
        dest: /opt/apache-tomcat-8.5.35/webapps
```
*copyfile.yml will be triggered through jenkins.
