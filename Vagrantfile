# -*- mode: ruby -*-
# vi: set ft=ruby :
hosts = {
  "k8s-master" => "199.152.78.17",
  "k8s-slave1" => "199.152.78.18",
  "k8s-slave2" => "199.152.78.19"
}
Vagrant.configure("2") do |config|
  # always use Vagrants insecure key
  config.ssh.insert_key = false
  # forward ssh agent to easily ssh into the different machines
  config.ssh.forward_agent = true

  check_guest_additions = false
  functional_vboxsf     = false

  config.vm.box = "ubuntu/bionic64"
  hosts.each do |name, ip|
    config.vm.hostname = name
    config.vm.define name do |machine|
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do  |v|
        v.name = name
      end
    end
    config.vm.provision "shell", inline: "sudo apt update && sudo apt install -y python-minimal sshpass"
  end
end
