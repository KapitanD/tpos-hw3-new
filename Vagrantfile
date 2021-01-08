# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'etc'

@ip = "192.168.10.20"
puts "This script will start these VMs:"
puts "%s-nginx-server with IP %s" % [Etc.getlogin, @ip]

$update_ubuntu = <<SCRIPT
apt install python-dev python3-dev -y
SCRIPT

Vagrant.configure("2") do |config|
  config.hostmanager.enabled = false
  config.hostmanager.manage_guest = true
  config.hostmanager.include_offline = true
  config.hostmanager.ignore_private_ip = false
  config.ssh.forward_agent = true
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.define :main do |main|
    main.vm.box = "ubuntu/bionic64"
    main.vm.provider "virtualbox" do |vb|
      vb.cpus = "1"
      vb.memory = "1024"
    end
    main.vm.network :private_network, ip: @ip
    main.vm.hostname = Etc.getlogin + "-nginx-server"
    main.vm.provision "file", source: "./ssh-keys/ansible-hw.pub", destination: "~/.ssh/me.pub"
    main.vm.provision "shell", inline: <<-SHELL
        cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
    main.vm.provision :hostmanager
    main.vm.provision :shell, :inline => $update_ubuntu
  end  
end
