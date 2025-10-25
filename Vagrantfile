# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.hostname = "yolo-dev"

  # Forward port 3000
  config.vm.network "forwarded_port", guest: 3000, host: 3000
