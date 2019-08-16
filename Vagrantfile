# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 2.0"

Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"

    # If true, Vagrant will automatically insert a keypair to use for SSH,
    # replacing Vagrant's default insecure key inside the machine if detected.
    # By default, this is true.
    config.ssh.insert_key = false

    # config.ssh.forward_agent = true

    # SSH port is forwarded by default
    # config.vm.network "forwarded_port", guest: 22, host: 2222

    # Sync Vagrant root to provide ansible.cfg file
    config.vm.synced_folder ".", "/vagrant", type: "rsync",
        rsync__auto: false,
        rsync__exclude: ".git/"

    config.vm.provision "shell", inline: <<-SHELL
        # Install EPEL repository - Extra Packages for Enterprise Linux 7
        yum -y install epel-release

        # Install Ansible from EPEL repo
        yum -y install ansible
    SHELL

    # Web server machine definition
    config.vm.define "aem", primary: true do |machine|
        machine.vm.hostname = "aem"
        machine.vm.network "private_network", ip: "192.168.33.12"
        machine.vm.network "forwarded_port", guest: 4502, host: 4502
        machine.vm.provider "virtualbox" do |vb|
            vb.name = "vagrant_ansible_aem"
            vb.gui = false
            vb.memory = "1536"
            vb.cpus = 1
        end
        machine.vm.provision :ansible_local do |ansible|
            ansible.verbose = "vvv"
            ansible.compatibility_mode = "2.0"
            ansible.playbook = "./provisioning/aem_playbook.yml"
            ansible.inventory_path = "./provisioning/development.yml"
        end
    end
end
