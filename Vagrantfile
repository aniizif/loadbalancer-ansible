# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.gui=false
    vb.memory=512
    vb.cpus=1
    vb.check_guest_additions=false
    config.vm.box_check_update=false
    config.vm.box="ubuntu/jammy64"
  end

  (1..3).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.network "private_network", ip: "192.168.1.#{24+i}"
      node.vm.hostname="node#{i}"

      node.vm.provision "shell", inline: <<-SHELL
        sudo sed -i 's/^#\\?PasswordAuthentication.*/PasswordAuthentication yes/' '/etc/ssh/sshd_config'
        sudo systemctl restart sshd
      SHELL
    end
  end
end
