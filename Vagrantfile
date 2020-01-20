# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  ## Escolha da Box
  config.vm.box = "ubuntu/bionic64"

  ## WORKSPACE
  config.vm.define 'workspace' do |workspace|
    workspace.vm.hostname = "workspace"
    workspace.vm.network "forwarded_port", guest: 8080, host: 8080

    # Configurações de Size da VM
    workspace.vm.provider "virtualbox" do |v|
      v.name = "workspace"
      v.memory = 1024
      v.cpus = 2
    end

    # Instala as Roles
    workspace.vm.provision :ansible_local do |ansible|
        ansible.install_mode = "default"
        ansible.playbook = "workspace-ansible/pre-playbook.yml"
        ansible.verbose  = true
        ansible.install  = true
        ansible.limit    = "all" 
        ansible.inventory_path = "workspace-ansible/inventory"
    end

    # Configura a Workspace
    workspace.vm.provision :ansible_local do |ansible|
        ansible.install_mode = "default"
        ansible.playbook = "workspace-ansible/playbook.yml"
        ansible.verbose  = true
        ansible.install  = true
        ansible.limit    = "all" 
        ansible.inventory_path = "workspace-ansible/inventory"
    end

  end

end
