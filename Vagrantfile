# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "web" do |node|
    node.vm.box = "bento/ubuntu-20.04"
    node.vm.hostname = "web"
    node.vm.network "public_network", ip: "192.168.0.3", netmask: "255.255.255.0", bridge: "en0: Ethernet" # ethnet of mac
    # node.vm.network "public_network", ip: "192.168.0.3", netmask: "255.255.255.0", bridge: "en1: Wi-Fi (AirPort)" # wifi of mac
    node.vm.synced_folder "./html", "/var/www/html", :mount_options => [ "dmode=777", "fmode=777" ]
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
    # ansible.playbook = "install_docker.yml"
    ansible.inventory_path = "inventory.ini"
    ansible.limit = 'all'
  end

end
