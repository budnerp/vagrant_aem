# vagrant_aem
VirtualBox based VM integrated with Vagrant and Ansible for AEM development

## What's inside?
- Based on [centos/7](https://app.vagrantup.com/centos/boxes/7) box
    - Python 2.7
- Defaults: 
    - Ansible (local) 2.x installed 
    - Machine "aem":
        - private_network, ip: 192.168.33.12
        - 1 CPU, 1536MB of memory
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
    git clone https://github.com/budnerp/vagrant_ansible.git
    git submodule init
    git submodule update
    vagrant up
    ```
3. Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
    ```
    192.168.33.12 aem.local
    ```
4. Coffee sip :)
5. SSH into the instance. Execute:
    ```
    vagrant ssh aem
    ```
6. Setup GIT config (if ansible_role_git is a part of playbook)
    ```
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
    ```

## License
Copyright (c) We Are Interactive under the MIT license.

