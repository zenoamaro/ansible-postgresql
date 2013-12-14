# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure '2' do |config|


	# PostgreSQL standalone box
	# -------------------------

	# Provision this machine to obtain a standalone box
	# with a pgsql inside listening on the default port.

	config.vm.define 'boxed', primary: true do |box|
		box.vm.box     = "precise64"
		box.vm.box_url = "https://s3.amazonaws.com/gsc-vagrant-boxes/ubuntu-12.04-omnibus-chef.box"

		# Configure the network topology to your needs
		config.vm.network :private_network, ip: "192.168.33.20"
		# config.vm.network :public_network

		# Provision this as a PostgreSQL box, so to be able to
		# listen on the outside.
		config.vm.provision :ansible do |ansible|
			ansible.playbook       = './boxed.yml'
			ansible.inventory_path = './inventory'
		end

		# Forward this postgres to a port on the host
		# config.vm.network :forwarded_port, guest: 5432, host: 15432
	end


	# Test machines
	# -------------

	# These test machines will configure PostgreSQL with all
	# its extensions enabled, in order to test the validity
	# of the role.
	#
	# The only machine available at the moment is "test-ubuntu-precise"

	def apply_test_vm_defaults(config)
		config.vm.network :private_network, ip: "192.168.33.20"
	end

	def apply_test_ansible_defaults(ansible)
		ansible.playbook       = './test.yml'
		ansible.inventory_path = './inventory'
	end

	config.vm.define 'test-ubuntu-precise' do |box|
		box.vm.box     = "precise64"
		box.vm.box_url = "https://s3.amazonaws.com/gsc-vagrant-boxes/ubuntu-12.04-omnibus-chef.box"
		apply_test_vm_defaults box
		config.vm.provision :ansible do |ansible|
			apply_test_ansible_defaults ansible
			ansible.extra_vars = {}
		end
	end

end
