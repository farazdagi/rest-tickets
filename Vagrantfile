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
        app.vm.synced_folder "./projects/app", "/project", type: "nfs"
    end

    # Database Server
    config.vm.define "db" do |db|
        db.vm.box = "precise64"
        db.vm.box_url = "http://files.vagrantup.com/precise64.box"
        db.vm.hostname = "db"
        db.vm.network :private_network, ip: "10.3.0.20"
        db.vm.synced_folder "./projects/db", "/project", type: "nfs"
    end

    # API Server
    config.vm.define "api" do |api|
        api.vm.box = "precise64"
        api.vm.box_url = "http://files.vagrantup.com/precise64.box"
        api.vm.hostname = "api"
        api.vm.network :private_network, ip: "10.3.0.30"
        api.vm.synced_folder "./projects/api", "/project", type: "nfs"

        # Provision with Ansible (Once the last node is ready)
        config.vm.provision :ansible do |ansible|
            ansible.playbook = "site.yml"
            ansible.inventory_path = "hosts"
        end
    end

    # Provider(s) configuration
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
end