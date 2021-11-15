# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "node1" do |node1|
    node1.vm.box = "centos/7"
    node1.vm.hostname = "node1.example.com"
    node1.vm.network "private_network", ip: "172.16.16.100"
    node1.vm.provider "virtualbox" do |v|
      v.name = "node1"
      v.memory = 2048
      v.cpus = 2
      # Prevent VirtualBox from interfering with host audio stack
      v.customize ["modifyvm", :id, "--audio", "none"]
    end
    node1.vm.provider :libvirt do |v|
      v.memory = 2048
      v.nested = true
      v.cpus = 2
    end
  #  kmaster.vm.provision "shell", path: "bootstrap_kmaster.sh"
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "worker#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "worker#{i}.example.com"
      workernode.vm.network "private_network", ip: "172.16.16.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "worker#{i}"
        v.memory = 1024
        v.cpus = 1
        # Prevent VirtualBox from interfering with host audio stack
        v.customize ["modifyvm", :id, "--audio", "none"]
      end
      workernode.vm.provider :libvirt do |v|
        v.memory = 1048
        v.nested = true
        v.cpus = 1
      end
    end
  end 
end
