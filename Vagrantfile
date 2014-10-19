# -*- mode: ruby -*-
# vi: set ft=ruby :

required_plugins = %w( vagrant-exec )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
  end

$setup_script = <<SCRIPT
# install node.js, nvm, git
apt-get update
apt-get install -y nodejs nodejs-legacy npm git

# install grunt-cli
npm install -g grunt-cli

cd /vagrant
npm install
SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty32"
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  config.vm.network "forwarded_port", guest: 35729, host: 35729

  config.vm.provision "shell", inline: $setup_script
end
