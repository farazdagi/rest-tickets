# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    # Application Server
    config.vm.define "app" do |app|
        app.vm.box = "precise64"
        app.vm.box_url = "http://files.vagrantup.com/precise64.box"
        app.vm.hostname = "app"
        app.vm.network :private_network, ip: "10.3.0.10"
        app.vm.synced_folder "./projects/app", "/project", type: "nfs"  # NFS requires password during 'vagrant up'

        # Provision with Ansible
        app.vm.provision :ansible do |ansible|
            ansible.playbook = "site.appservers.yml"
            ansible.inventory_path = "hosts"
            ansible.limit = 'all'
        end
    end

    # Database Server
    config.vm.define "db" do |db|
        db.vm.box = "precise64"
        db.vm.box_url = "http://files.vagrantup.com/precise64.box"
        db.vm.hostname = "db"
        db.vm.network :private_network, ip: "10.3.0.20"
        db.vm.synced_folder "./projects/db", "/project", type: "nfs"

        # Provision with Ansible
        db.vm.provision :ansible do |ansible|
            ansible.playbook = "site.dbservers.yml"
            ansible.inventory_path = "hosts"
            ansible.limit = 'all'
        end
    end

    # API Server
    config.vm.define "api" do |api|
        api.vm.box = "precise64"
        api.vm.box_url = "http://files.vagrantup.com/precise64.box"
        api.vm.hostname = "api"
        api.vm.network :private_network, ip: "10.3.0.30"
        api.vm.synced_folder "./projects/api", "/project", type: "nfs"

        # Provision with Ansible
        api.vm.provision :ansible do |ansible|
            ansible.playbook = "site.apiservers.yml"
            ansible.inventory_path = "hosts"
            ansible.limit = 'all'
        end
    end

    # Provider(s) configuration
    config.vm.provider "virtualbox" do |v|
      v.customize ['--memory', '256']
    end

end
