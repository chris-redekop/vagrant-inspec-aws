# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "inspec-aws"
  end

  config.vm.provision "file", source: "ssh/config", destination: ".ssh/config" 
  config.vm.provision "file", source: "ssh/id_rsa", destination: ".ssh/id_rsa" 
  config.vm.provision "file", source: "ssh/id_rsa.pub", destination: ".ssh/id_rsa.pub" 
  config.vm.provision "file", source: "etc/aws-vars", destination: "/tmp/aws-vars" 

  config.vm.provision "shell", inline: <<-SHELL
    chmod 400 /home/ubuntu/.ssh/id_rsa

    apt-get update
    apt-get install -y git unzip zlib1g-dev bundler

    pushd /tmp
      wget -q https://packages.chef.io/files/stable/chefdk/1.1.16/ubuntu/14.04/chefdk_1.1.16-1_amd64.deb
      dpkg -i chefdk_1.1.16-1_amd64.deb 
      rm chefdk_1.1.16-1_amd64.deb

      wget -q https://releases.hashicorp.com/terraform/0.9.6/terraform_0.9.6_linux_amd64.zip
      unzip terraform_0.9.6_linux_amd64.zip -d /usr/bin
      rm terraform_0.9.6_linux_amd64.zip

      cat aws-vars >> /etc/environment
      rm aws-vars
    popd

    sed -ie 's#"$#:/opt/chefdk/bin"#' /etc/environment

    sudo -i -u ubuntu sh -c 'ssh-keyscan github.com >> ~/.ssh/known_hosts'
    sudo -i -u ubuntu sh -c 'cd /home/ubuntu && git clone git@github.com:chef/inspec-aws.git'
  SHELL
end
