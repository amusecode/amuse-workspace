# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/ubuntu2004"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus   = 1
  end
  
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "vagrant-provision.yml"
    ansible.become = true
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "research-cloud-plugin.yml"
    ansible.become = true
  end

end

