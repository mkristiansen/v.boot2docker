# -*- mode: ruby -*-
# vi: set ft=ruby :
 
# Just in case you have something else configured
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'
 
# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "raring64"
  config.vm.box_url = 'http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box'
  config.vm.network :private_network, ip: "10.1.2.22"
  config.vm.synced_folder "../", "/docker"
  config.vm.hostname = "containers"
 
  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.auto_detect = true
  end
 
  config.vm.provider :virtualbox do |vb, override|
    vb.customize [ "modifyvm", :id, "--memory", 1536, "--cpus", "2" ]
  end
 
  # Install docker on the machine
  config.vm.provision :docker
 
  # Install Vagrant
  config.vm.provision :shell, inline: %[:wq
    if $(which vagrant > /dev/null 2>/dev/null); then
      exit 0
    fi
    wget https://dl.bintray.com/mitchellh/vagrant/vagrant_1.5.1_x86_64.deb -O /tmp/vagrant.deb
    dpkg -i /tmp/vagrant.deb
  ]
 
  # Install docker-provider
  config.vm.provision :shell, privileged: false, inline: %[
    if $(vagrant plugin list | grep -q 'docker-provider'); then
      exit 0
    fi
    vagrant plugin install docker-provider
    vagrant plugin install vagrant-omnibus
  ]
end