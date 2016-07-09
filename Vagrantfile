# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  # The web servers
  web_servers = []

  # Configure the Single Database server
  config.vm.define "database" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "database"

#    config.vm.provision :ansible do |ansible|
#      ansible.groups = {
#        "database" => ["database"],
#      }
#      ansible.playbook = "database.yml"
#      ansible.verbose = true
#      ansible.sudo = true
#      ansible.limit = "all"
#    end

  end

  # We are going to create 3 VMs
  (1..2).each do |i|

    # set a name for the VM
    vm_name="web#{i}"

    # add the server to web server list
    web_servers.push(vm_name)

    config.vm.define vm_name do |node|
      node.vm.box = "centos/7"
      node.vm.hostname = vm_name
    end

    config.vm.provision :ansible do |ansible|
      ansible.groups = {
        "webservers" => web_servers,
      }
      ansible.playbook = "web.yml"
      ansible.verbose = true
      ansible.sudo = true
      ansible.limit = "all"
    end

  end

  # configures the machine for 
  config.vm.provider :libvirt do |libvirt|
    libvirt.nested = true
    libvirt.driver = "kvm"
  end
end
