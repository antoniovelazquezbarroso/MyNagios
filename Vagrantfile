# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure(2) do |config|

  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end


  config.vm.define "myruby" do |ubuntu1404|

    ubuntu1404.vm.box = "geerlingguy/ubuntu1404"
    ubuntu1404.vm.hostname = "myruby"    
    ubuntu1404.vm.network :private_network, ip: "192.168.2.11"
  end


  config.vm.define "ubuntu1404" do |ubuntu1404|

    ubuntu1404.vm.box = "geerlingguy/ubuntu1404"
    ubuntu1404.vm.hostname = "ubuntu1404"    
    ubuntu1404.vm.network :private_network, ip: "192.168.2.10"

    ubuntu1404.vm.provision "ansible" do |ansible|
      ansible.playbook = "./playbooks/playbook.yml"
      ansible.inventory_path = "./playbooks/inventory-ansible"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end

  end


end
