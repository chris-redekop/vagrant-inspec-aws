# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "inspec-aws"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get purge -y ruby
    pushd /tmp
      wget -q https://packages.chef.io/files/stable/chefdk/1.1.16/ubuntu/14.04/chefdk_1.1.16-1_amd64.deb
      dpkg -i chefdk_1.1.16-1_amd64.deb 
    popd
    apt-get install -y git
    sed -e 's#"$#:/opt/chefdk/embedded/bin"#' /etc/environment
  SHELL
end
