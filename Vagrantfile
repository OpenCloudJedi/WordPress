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


  # server1.
  config.vm.define "server1" do |server1|
    server1.vm.hostname = "server1.test"
    server1.vm.network :private_network, ip: "192.168.2.3"

    server1.vm.provision "shell",
      inline: "sudo yum update -y"

    server1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 768]
    end
  end

  # Server2.
  config.vm.define "server2" do |server2|
    server2.vm.hostname = "server2.test"
    server2.vm.network :private_network, ip: "192.168.2.4"

    server2.vm.provision "shell",
      inline: "sudo yum update -y"

    server2.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 768]
    end
  end


   # # Run Ansible provisioner once for all VMs at the end.
   # memcached.vm.provision "ansible" do |ansible|
   #   ansible.playbook = "configure.yml"
   #   ansible.inventory_path = "inventories/vagrant/inventory"
   #   ansible.limit = "all"
   #   ansible.extra_vars = {
   #     ansible_user: 'vagrant',
   #     ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
   #   }
   # end
  #end
end

# Gnome box.
config.vm.provider :virtualbox do |v|
  v.memory = 2048
  v.cpus = 1
  v.linked_clone = true
  v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  v.customize ["modifyvm", :id, "--ioapic", "on"]
end
# Workstation.
config.vm.define "workstation" do |workstation|
  workstation.vm.hostname = "workstation.test"
  workstation.vm.network :private_network, ip: "192.168.2.5"

  config.vm.box = "kane_project/centos8gui"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true
  workstation.vm.provision "shell",
    inline: "sudo yum update -y"

  server2.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", 2048]
  end
end
