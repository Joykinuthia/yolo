# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.hostname = "yolo-dev"

  # Forward port 3000
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # VirtualBox settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  # Ansible provisioning
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "hosts"
    ansible.become = true
    ansible.verbose = "vv"
    ansible.compatibility_mode = "2.0"
  end
end
