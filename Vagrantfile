# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # You MUST include a link to insecure_private_key if you set
  #   insert_key to false.
  config.ssh.insert_key = false
  config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"

  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.provider :virtualbox do |v|
    v.memory = 3076
    v.linked_clone = true
    # Kludge -- Don't write log -- crashes
    v.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end

  # Ubuntu Server
  config.vm.define "p0.ubuntu" do |p0_ubuntu|
    p0_ubuntu.vm.box = "ubuntu/bionic64"
    p0_ubuntu.vm.hostname = "p0.ubuntu"
    p0_ubuntu.vm.network :private_network, ip: "192.168.60.4"

    p0_ubuntu.vm.provision "ansible" do |ansible|
      ansible.playbook = "main.yml"
    end
  end
end
