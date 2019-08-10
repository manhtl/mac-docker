# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder "../../", "/vagrant_data", :type => "nfs", mount_options:['nolock,vers=3,udp,noatime,actimeo=1']

  config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2576]
      v.customize ["modifyvm", :id, "--name", "dockerdev"]
      v.customize ["modifyvm", :id, "--cpus", 2]
  end
 
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum install -y yum-utils \
      device-mapper-persistent-data \
      lvm2 \
      curl
    sudo yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo
    sudo yum-config-manager --disable docker-ce-edge
    sudo yum install -y docker-ce
    sudo systemctl start docker
    sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    sudo usermod -a -G docker $USER
    sudo systemctl enable docker
  SHELL
  # config.vm.provision :shell, path: "bootstrap.sh"
  config.ssh.forward_agent = true
end
