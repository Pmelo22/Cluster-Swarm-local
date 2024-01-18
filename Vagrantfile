# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Definição da máquina master
  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.network "private_network", ip: "192.168.56.10"
    master.vm.hostname = "master"
    master.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      systemctl start docker
      systemctl enable docker
      docker swarm init --advertise-addr 192.168.56.10
    SHELL
  end

  # Definição das máquinas workers
  (1..3).each do |i|
    config.vm.define "node0#{i}" do |node|
      node.vm.box = "ubuntu/bionic64"
      node.vm.network "private_network", ip: "192.168.56.1#{i}"
      node.vm.hostname = "node0#{i}"
      node.vm.provision "shell", inline: <<-SHELL
        apt-get update
        apt-get install -y docker.io
        systemctl start docker
        systemctl enable docker
      SHELL
    end
  end
end
