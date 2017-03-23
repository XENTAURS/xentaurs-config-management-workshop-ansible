# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.8.0"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"

  # First, install python
  config.vm.provision "shell" do |s|
    s.inline = "apt-get install -y python"
  end

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = ".vagrant.yml"
  end
  config.vm.provision :serverspec do |spec|
    spec.pattern = 'serverspec/roles/*/*_spec.rb'
  end
end
