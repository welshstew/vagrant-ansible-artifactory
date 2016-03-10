# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.8.0"

# Install required Vagrant plugins
missing_plugins_installed = false
required_plugins = %w(vagrant-vbguest vagrant-hostmanager vagrant-cachier vagrant-registration vagrant-adbinfo)

required_plugins.each do |plugin|
  if !Vagrant.has_plugin? plugin
    system "vagrant plugin install #{plugin}"
    missing_plugins_installed = true
  end
end

# If any plugins were missing and have been installed, re-run vagrant
if missing_plugins_installed
  exec "vagrant #{ARGV.join(" ")}"
end

Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "./shared_data", "/shared_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end

  config.cache.scope = :box

  # Config /etc/hosts via plugin
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  # OSE Master VM
  config.vm.define :artifactory do |artifactory|
    # Assign network config
    artifactory.vm.hostname = "artifactory.vagrant.local"
    artifactory.vm.network "private_network", ip: "10.1.2.22"

    # Share a folder
    artifactory.vm.synced_folder "~/share/artifactory", "/home/vagrant/share/artifactory"

    # Config the box
    artifactory.vm.provision "ansible" do  |ansible|
      ansible.playbook = "provisioners/docker.yml"
    end

    # Complete message
    artifactory.vm.post_up_message = "https://artifactory.vagrant.local:8080/"
  end

  




  # # Ansible provisioner example using docker.yml

  # config.vm.provision "ansible" do |ansible|
  #   ansible.playbook = "provisioners/docker.yml"
  # end
  
end
