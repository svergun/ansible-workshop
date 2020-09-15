# -*- mode: ruby -*-
# vi: set ft=ruby :
$hostsfile_update = <<-'SCRIPT'
echo -e '192.168.56.100 control.example.com control\n192.168.56.101 node1.example.com node1\n192.168.56.102 node2.example.com node2' >> /etc/hosts
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config && systemctl restart sshd
SCRIPT

$control_update = <<-'SCRIPT'
yum -y install epel-release git bind-utils lsof libselinux-python mc net-tools nmap-ncat python3-pip tar telnet tree vim wget zip sshpass
SCRIPT

$node_update = <<-'SCRIPT'
yum -y install epel-release libselinux-python python3-pip tar vim zip
SCRIPT

$control_user_configure = <<-'SCRIPT'
ssh-keygen -b 2048 -t rsa -f /home/vagrant/.ssh/id_rsa -q -N ""
echo -e "Host node*\n  StrictHostKeyChecking no\n  UserKnownHostsFile /dev/null\n  User vagrant\n" > .ssh/config
chmod 600 .ssh/config
sshpass -p 'vagrant' ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@node1
sshpass -p 'vagrant' ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@node2
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define "node1" do |node1|
    node1.vm.box = "centos/7"
    node1.vm.hostname = "node1.example.com"
    node1.vm.network "private_network", ip: "192.168.56.101"
    node1.vm.provision "shell", inline: $hostsfile_update
    node1.vm.provision "package", type: "shell", inline: $node_update
    node1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "centos/7"
    node2.vm.hostname = "node2.example.com"
    node2.vm.network "private_network", ip: "192.168.56.102"
    node2.vm.provision "shell", inline: $hostsfile_update
    node2.vm.provision "package", type: "shell", inline: $node_update
    node2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
  end

  config.vm.define "control", primary: true do |control|
    control.vm.box = "centos/7"
    control.vm.hostname = "control.example.com"
    control.vm.network "private_network", ip: "192.168.56.100"
    control.vm.synced_folder ".", "/vagrant"
    control.vm.provision "hosts", type: "shell", inline: $hostsfile_update
    control.vm.provision "package", type: "shell", inline: $control_update
    control.vm.provision "user", type: "shell", privileged: false, inline: $control_user_configure
    control.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
  end

end
