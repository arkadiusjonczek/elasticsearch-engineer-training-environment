BOX_IMAGE = "ubuntu/xenial64"

$script = <<-SCRIPT
echo "192.168.10.2 server1" >> /etc/hosts
echo "192.168.10.3 server2" >> /etc/hosts
echo "192.168.10.4 server3" >> /etc/hosts
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"

  config.vm.define "server1" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "server1"
    subconfig.vm.network :private_network, ip: "192.168.10.2"
    subconfig.vm.provision "shell", inline: $script
  end

  config.vm.define "server2" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "server2"
    subconfig.vm.network :private_network, ip: "192.168.10.3"
    subconfig.vm.provision "shell", inline: $script
  end

  config.vm.define "server3" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "server3"
    subconfig.vm.network :private_network, ip: "192.168.10.4"
  end
end
