Vagrant.configure("2") do |config|
  config.vm.provider "docker" do |d|
    d.cmd     = ["/sbin/my_init", "--enable-insecure-key"]
    d.image   = "phusion/baseimage"
    d.has_ssh = true
  end

  config.ssh.username = "root"
  config.ssh.private_key_path = "~/.keys/insecure_key"

config.vm.provision "shell", inline: "echo Hello"

end