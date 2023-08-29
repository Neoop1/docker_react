# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "dockersrv" do |dockersrv|
    dockersrv.vm.box = "ubuntu/focal64"
    dockersrv.vm.network "private_network", ip: "192.168.58.100"
    dockersrv.vm.synced_folder "./docker_files","/home/vagrant/docker_files"
    dockersrv.vm.hostname =  "dockersrv"
    dockersrv.vm.provider "virtualbox" do |vb|
      vb.memory = "2024"
    end
    config.vm.provision "file", source: 'sshkey/ssh_key', destination: "/home/vagrant/.ssh/"
    config.vm.provision "file", source: 'sshkey/ssh_key.pub', destination: "/home/vagrant/.ssh/"
    dockersrv.vm.provision "shell", inline: <<-SHELL
      sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/#g' /etc/ssh/sshd_config
      sed -i -e '$aPermitRootLogin yes' /etc/ssh/sshd_config
      service ssh restart
      chmod 600 /home/vagrant/.ssh/ssh_key
      cat /home/vagrant/.ssh/ssh_key.pub >> /home/vagrant/.ssh/authorized_keys
      SHELL
  end
end
