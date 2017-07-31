# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "bento/centos-7.3"
  config.vm.hostname = "RedmineDev"
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 18080, host: 18080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./redmine-docker-template", "/redmine-docker-template"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  
    # Customize the amount of memory on the VM:
    vb.memory = "2048"

    docker_disk = './additional-disk-volume.vdi'
    unless File.exists?(docker_disk)
      vb.customize ['createhd', '--filename', docker_disk, '--size', 50 * 1024]
    end
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', docker_disk]
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  config.vm.provision "shell", inline: <<-SHELL
    # Add an XFS+LVM disk and mount it to /opt/docker.
    parted /dev/sdb --script -- mklabel msdos
    parted /dev/sdb --script -- mkpart primary 0% 100%
    pvcreate /dev/sdb1
    vgcreate docker /dev/sdb1
    lvcreate -l +100%FREE -n docker docker
    mkfs.xfs /dev/docker/docker
    mkdir /opt/docker
    echo '/dev/mapper/docker-docker /opt/docker xfs defaults 0 0' >> /etc/fstab
    mount /opt/docker

    # Package initialization.
    yum -y update

    # Install Docker.
    curl -fsSL get.docker.com | sh

    # Enable and start Docker.
    systemctl enable docker.service
    systemctl start docker.service

    # Install docker-compose.
    curl -L https://github.com/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > /usr/bin/docker-compose
    chmod +x /usr/bin/docker-compose

    # Install other tools. (Optional)
    yum -y install git

    # Copy redmine-docker-template.
    cp -r /redmine-docker-template/* /opt/docker

    # Run docker-compose.
    cd /opt/docker
    docker-compose up -d
  SHELL
end
