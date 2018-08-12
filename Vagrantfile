# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  $OS = 'bento/ubuntu-16.04';
  # $OS = 'bento/centos-6.9';
  config.vm.box = $OS

  $script = <<-SCRIPT
    sudo yum install kernel* -y
  SCRIPT

  $loadbalancer_ip = "192.168.2.3"

  config.vm.provider "virtualbox" do |apache|
    apache.linked_clone = true
    apache.memory = "512"
  end


  config.vm.network "public_network"
  config.ssh.insert_key = false

  backendPool = [
      {:name => "server01", :ip => '192.168.2.5'},
      {:name => "server02", :ip => '192.168.2.6'},
      {:name => "server03", :ip => '192.168.2.7'},
      # {:name => "server04", :ip => '192.168.2.8'}
  ]

  backendPool.each do |server|
    config.vm.define server[:name], primary: true do |v|
      v.vm.hostname = server[:name]
      v.vm.network :private_network, ip: server[:ip]
    end
  end


  config.vm.define "loadbalancer" do |v|
    v.vm.hostname = "loadbalancer.local"
    v.vm.network :private_network, ip: $loadbalancer_ip
  end


  config.vm.define "ansible_controller", primary: true do |v|
    v.vm.network :private_network, ip: "192.168.2.65"
  
    v.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/deploy.yml"
      ansible.inventory_path = "inventory"
      ansible.config_file = "ansible.cfg"
      ansible.limit = "all"
    end
  end


end 