# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  config.vm.define 'zookeeper' do |zookeeper|

  		zookeeper.vm.hostname = "zookeeper.dev"
		zookeeper.vm.box = "hfm4/centos7"
		zookeeper.vm.network "private_network", ip: "192.168.33.10"

		zookeeper.ssh.forward_agent = true

		zookeeper.vm.provider "virtualbox" do |vb|
			vb.customize ["modifyvm", :id, "--memory", "1024"]
		end 
	end 

	config.vm.define 'kafka' do |kafka|
		kafka.vm.hostname = "kafka.dev"
		kafka.vm.box = "hfm4/centos7"
		kafka.vm.network "private_network", ip: "192.168.33.11"

		kafka.ssh.forward_agent = true

		kafka.vm.provider "virtualbox" do |vb|
			vb.customize ["modifyvm", :id, "--memory", "1024"]
		end

		kafka.vm.provision "ansible" do |ansible|
			ansible.playbook = "configure.yml"
			ansible.inventory_path = "inventory"
			ansible.limit = 'all'
			ansible.extra_vars = {
				ansible_ssh_user: 'vagrant',
				ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
			}
		end 
	end
end
  
