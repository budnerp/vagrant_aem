# Vagrant and Ansible for Adobe Experience Manager
VirtualBox based VM integrated with Vagrant and Ansible for AEM development

## What's inside?
- Based on [centos/7](https://app.vagrantup.com/centos/boxes/7) box
    - Python 2.7
- Defaults: 
    - Ansible (local) 2.x installed 
    - Machine "aem":
        - private_network, ip: 192.168.33.12
        - 2 CPU, 4096MB of memory
        - SSH on port 22
- Epel and Remi's RPM repositories
- Common tools: `htop`, `vim`, `nano`, `mc`, `lsof`, `wget`, `zip`, `unzip`
- GIT 2.9
- SELinux disabled

## Prerequisities
- Git
- rsync (or rsync.exe) on the path
- Vagrant ver. >= 2.0
- Virtual Box ver. >= 2.0

## Tested on

## Installation
1. Install VirtualBox Guest Additions plugin
    ```
    vagrant plugin install vagrant-vbguest
    ```
2. Clone repository, pull sub-modules and start provisioning
    ```
    git clone https://github.com/budnerp/vagrant_aem.git
    git submodule init
    git submodule update
    ```
3. Replace `provisioning/roles/ansible_role_aem/templates/aem/replace-this-with-AEM_6.5_Quickstart.jar.txt` file with valid `AEM_6.5_Quickstart.jar` file.
4. Replace `provisioning/roles/ansible_role_aem/templates/aem/replace-this-with-license.properties-file.txt` file with valid `license.properties` file.
5. Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
    ```
    192.168.33.12 aem.local
    ```
6. SSH into the instance. Execute:
    ```
    vagrant ssh aem
    ```
7. (Optional) Setup GIT config (if ansible_role_git is a part of playbook)
    ```
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
    ```
8. To start AEM author instance execute:
    ```
    sudo /opt/aem/author/crx-quickstart/bin/start
    ```
    To start AEM publish instance:
    ```
    sudo /opt/aem/publish/crx-quickstart/bin/start
    ```
9. Wait until services are up (this might take a while).

## AEM manual, raw installation guide
Upload `AEM_6.5_Quickstart.jar` and `license.properties` into `/home/vagrant/`
```
cd /home/vagrant/ 
sudo mkdir /opt/aem
sudo mkdir /opt/aem/author
sudo mkdir /opt/aem/publish
sudo cp AEM_6.5_Quickstart.jar /opt/aem/author/aem-author-p4502.jar
sudo cp AEM_6.5_Quickstart.jar /opt/aem/publish/aem-publish-p4503.jar
sudo cp license.properties /opt/aem/author/
sudo cp license.properties /opt/aem/publish/
cd /opt/aem
sudo chown -R vagrant:vagrant .
sudo chmod -R 0777 .
ls -la
cd author
java -jar aem-author-p4502.jar -unpack
cd ../publish
java -jar aem-publish-p4503.jar -unpack
cd /
/opt/aem/author/crx-quickstart/bin/start
/opt/aem/publish/crx-quickstart/bin/start
```

wait and check in browser
 
Publish: http://192.168.33.12:4503/

Author: http://192.168.33.12:4502/

Credentials admin:admin

## Links
Set up a Local AEM Development Environment https://helpx.adobe.com/experience-manager/kt/platform-repository/using/local-aem-dev-environment-article-setup.html
https://github.com/adobe/aem-cif-project-archetype

## License
Copyright (c) We Are Interactive under the MIT license.

