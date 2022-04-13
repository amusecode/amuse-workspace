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

  # forward port; host can access guest web server at port 8000
  config.vm.network "forwarded_port", guest: 8000, host: 8000, host_ip: "127.0.0.1"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus   = 1
  end

  # allow password login
  config.vm.provision "shell", inline: <<-SHELL
     sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
     systemctl restart sshd.service
  SHELL
  
  # pre-provision things available at the RSC
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "vagrant-provision.yml"
    ansible.become = true
  end

  # Provision the SRC plugin
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "application-jupyter.yml"
    ansible.become=true
  end

  # this is our plugin
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "research-cloud-plugin.yml"
    ansible.become = true
    #ansible.extra_vars= { amuse_devel_install: true }
    ansible.extra_vars= { list_of_users: [["amuse", "amuse"]] }
  end

end

