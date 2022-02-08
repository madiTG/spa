# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'getoptlong'

opts = GetoptLong.new(
  [ '--build', GetoptLong::OPTIONAL_ARGUMENT ],
  [ '--deploy', GetoptLong::OPTIONAL_ARGUMENT ],
  [ '--instances', GetoptLong::OPTIONAL_ARGUMENT]
)

buildParameter=''
deployParameter=''
instancesParameter=''

opts.each do |opt, arg|
  case opt
    when '--build'
      buildParameter=arg
    when '--deploy'
      deployParameter=arg
    when '--instances'
      instancesParameter=arg
  end
end

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.provider "docker"
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  if buildParameter == 'true'
#      config.vm.provider "docker" do |d|
#         d.remains_running = false
#    d.image = "nginx:latest"
#    d.ports = ["8081:80"]
#    d.name = "nginx-container"
#         d.build_dir = "ci_dockerfile"
#         d.build_args = ["--build-arg", "TOKEN="+ENV['GITHUB_ACCESS_TOKEN']]
#      end
      config.vm.define "build" do |d|
        d.vm.provider "docker" do |d|
          d.remains_running = false
          d.build_dir = "ci_dockerfile"
          d.build_args = ["--build-arg", "TOKEN="+ENV['GITHUB_ACCESS_TOKEN']]
        end
      end
  end
  puts instancesParameter
  if deployParameter == 'true'  
      if instancesParameter == '1'
        config.vm.define "d1" do |d1|
          d1.vm.provider "docker" do |d1|
            d1.image = "quay.io/tomaszgaska/spa:latest"
            d1.ports = ["801:80"]
          end
        end
#        config.vm.provider "docker" do |d1|
#          d1.name = "node1"
#          d1.image = "quay.io/tomaszgaska/spa:latest"
#          d1.ports = ["801:80"]
#        end
      elsif instancesParameter == '2'
        config.vm.define "d1" do |d1|
          d1.vm.provider "docker" do |d1|
            d1.image = "quay.io/tomaszgaska/spa:latest"
            d1.ports = ["801:80"]
          end
        end
        config.vm.define "d2" do |d2|
          d2.vm.provider "docker" do |d2|
            d2.image = "quay.io/tomaszgaska/spa:latest"
            d2.ports = ["802:80"]
          end
        end

#        config.vm.provider "docker" do |d1|
#          d1.name = "node1"
#          d1.image = "quay.io/tomaszgaska/spa:latest"
#          d1.ports = ["801:80"]
#        end
#        config.vm.provider "docker" do |d2|
#          d2.name = "node2"
#          d2.image = "quay.io/tomaszgaska/spa:latest"
#          d2.ports = ["802:80"]
#        end
      elsif instancesParameter == '3'
        config.vm.define "d1" do |d1|
          d1.vm.provider "docker" do |d1|
            d1.image = "quay.io/tomaszgaska/spa:latest"
            d1.ports = ["801:80"]
          end
        end
        config.vm.define "d2" do |d2|
          d2.vm.provider "docker" do |d2|
            d2.image = "quay.io/tomaszgaska/spa:latest"
            d2.ports = ["802:80"]
          end
        end
        config.vm.define "d3" do |d3|
          d3.vm.provider "docker" do |d3|
            d3.image = "quay.io/tomaszgaska/spa:latest"
            d3.ports = ["803:80"]
          end
        end
      end
   end


#        config.vm.provider "docker" do |d1|
#          d1.image = "quay.io/tomaszgaska/spa:latest"
#          d1.ports = ["801:80"]
#        end
#        config.vm.provider "docker" do |d2|
#          d2.image = "quay.io/tomaszgaska/spa:latest"
#          d2.ports = ["802:80"]
#        end
#        config.vm.provider "docker" do |d3|
#          d3.image = "quay.io/tomaszgaska/spa:latest"
#          d3.ports = ["803:80"]
#        end
#  config.vm.profider "docker" do |d|
#     d.build_dir = "start_dockerfile"
#  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 801, host: 4567

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  # config.vm.synced_folder "../data", "/vagrant_data"

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

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
