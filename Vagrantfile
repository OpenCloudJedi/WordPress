# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "bento/centos-8.3"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # General VirtualBox VM configuration.
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 1
    v.linked_clone = true
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end


  # web1.
  config.vm.define "web1" do |web1|
    web1.vm.hostname = "web1.test"
    web1.vm.network :private_network, ip: "192.168.2.3"
    web1.vm.provision "ansible" do |ansible|
      ansible.playbook = "webserver.yml"
      ansible.inventory_path = "inventory"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
end
  
#    web1.vm.provision "shell",
#      inline: "sudo yum update -y"

    web1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 2048]
    end
  end

  # db1.
  config.vm.define "db1" do |db1|
    db1.vm.hostname = "db1.test"
    db1.vm.network :private_network, ip: "192.168.2.4"

    db1.vm.provision "ansible" do |ansible|
      ansible.playbook = "dbserver.yml"
      ansible.inventory_path = "inventory"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    #db1.vm.provision "shell",
    #  inline: "sudo yum update -y"

    db1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 2048]
    end
  end


end
end
