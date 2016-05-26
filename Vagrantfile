# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.ssh.username = 'vagrant'
  
  ENV['LC_ALL']="en_US.UTF-8"

  config.vm.define :production do |production|
    config.vm.network "forwarded_port", guest: 8000, host: 8000
    production.vm.provider :virtualbox do |vb|
        vb.customize [ "modifyvm", :id, "--name", "Tile-server","--memory", 4096 ]
    end
    config.vm.provision "ansible" do |ansible|
    ansible.host_key_checking = false
    ansible.sudo = true
    ansible_inventory_path = "inventory.ini"
        ansible.playbook = "playbook.yml"
    end
    config.vm.network :private_network, ip: "192.168.100.100"
  end

end
