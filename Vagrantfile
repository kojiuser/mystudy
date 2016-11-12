# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "CentOS71"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "private_network", ip: "192.168.33.201"
  config.vm.hostname = "mystudy"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "C:/mygitkraken/kojima/github/mystudy/mysynced", "/home/vagrant/mysynced", :mount_options => ['dmode=755', 'fmode=644']
#  config.vm.synced_folder "C:/mygitkraken/kojima/github/mystudy/mysynced", "/home/vagrant/mysynced", :mount_options => ['dmode=775', 'fmode=664']

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL

  config.vm.provision "shell", inline: <<-SHELL
    # yum
    #yum update -y
    yum install -y yum-plugin-priorities

    # group, user
    groupadd -g 501 kojima
    useradd -g kojima -u 501 kojima
    
    # ssh
    sudo mkdir -p /home/kojima/.ssh
    sudo cp -a /vagrant/mysynced/ssh/enish/kojima/authorized_keys2 /home/kojima/.ssh/.
    sudo cp -a /vagrant/mysynced/ssh/enish/kojima/id_dsa /home/kojima/.ssh/.
    sudo chmod 600 /home/kojima/.ssh/authorized_keys2
    sudo chmod 600 /home/kojima/.ssh/id_dsa
    sudo chmod 700 /home/kojima/.ssh
    sudo chown -R kojima:kojima /home/kojima/.ssh

    # chrony
    yum install -y chrony
    systemctl stop ntpd.service
    systemctl disable ntpd.service
    systemctl start chronyd.service
    systemctl enable chronyd.service
    #ps aux | grep ntpd
    #ps aux | grep chronyd
    #systemctl status ntpd.service
    #systemctl status chronyd.service
    #systemctl is-enabled ntpd.service
    #systemctl is-enabled chronyd.service

    #security
    systemctl stop firewalld
    systemctl disable firewalld
    #ps aux | grep firewalld
    #systemctl status firewalld
    #systemctl is-enabled firewalld

    # cron
    yum remove -y cronie-anacron
    yum install -y cronie-noanacron

    # other
    # timedatectl
    timedatectl set-timezone Asia/Tokyo
    #timedatectl
    yum install -y sysstat
    #sar -V
    yum install -y git
    #git --version
    #yum install -y telnet
    #sar -V

    # service
    # systemctl -a -t service
    # systemctl list-units -t service
    # systemctl list-unit-files -t service

  SHELL

end

