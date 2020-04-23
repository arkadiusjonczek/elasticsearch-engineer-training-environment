BOX_IMAGE = "ubuntu/xenial64"

$script_host = <<-SCRIPT
echo "192.168.10.2 server1" >> /etc/hosts
echo "192.168.10.3 server2" >> /etc/hosts
echo "192.168.10.4 server3" >> /etc/hosts
SCRIPT

$script_jre = <<-SCRIPT
sudo apt-get update && sudo apt-get -y install openjdk-9-jre && sudo apt-get clean
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--cpus", 2]
    vb.customize ["modifyvm", :id, "--memory", 2048]
  end

  config.vm.box = BOX_IMAGE
  config.vm.provision "shell", inline: $script_host
  config.vm.provision "shell", inline: $script_jre

  config.vm.define "server1" do |subconfig|
    subconfig.vm.hostname = "server1"
    subconfig.vm.network :private_network, ip: "192.168.10.2"
    subconfig.vm.network "forwarded_port", guest: 80, host: 81
    subconfig.vm.network "forwarded_port", guest: 443, host: 4431
    subconfig.vm.network "forwarded_port", guest: 9200, host: 9201
  end

  config.vm.define "server2" do |subconfig|
    subconfig.vm.hostname = "server2"
    subconfig.vm.network :private_network, ip: "192.168.10.3"
    subconfig.vm.network "forwarded_port", guest: 80, host: 82
    subconfig.vm.network "forwarded_port", guest: 443, host: 4432
    subconfig.vm.network "forwarded_port", guest: 9200, host: 9202
  end

  config.vm.define "server3" do |subconfig|
    subconfig.vm.hostname = "server3"
    subconfig.vm.network :private_network, ip: "192.168.10.4"
    subconfig.vm.network "forwarded_port", guest: 80, host: 83
    subconfig.vm.network "forwarded_port", guest: 443, host: 4433
    subconfig.vm.network "forwarded_port", guest: 9200, host: 9203
  end

end
