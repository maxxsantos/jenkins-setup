# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/jammy64"

    # Jenkins VM
    config.vm.define "jenkins" do |jenkins|
        jenkins.vm.hostname = "jenkins.local"
        jenkins.vm.network "private_network", ip: "192.168.56.10"
        jenkins.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: true
        jenkins.vm.provider "virtualbox" do |vb|
            vb.name = "jenkins.service"
            vb.gui = false
            vb.memory = "2048"
            vb.cpus = "6"
        end
        jenkins.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbooks/jenkins/main.yml"
            ansible.inventory_path = "playbooks/jenkins/inventory"
        end
    end

    # Container Registry VM
    config.vm.define "registry" do |registry|
        registry.vm.hostname = "registry.local"
        registry.vm.network "private_network", ip: "192.168.56.11"
        registry.vm.provider "virtualbox" do |vb|
            vb.name = "registry.service"
            vb.gui = false
            vb.memory = "2048"
            vb.cpus = "2"
        end
        registry.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbooks/container-registry/main.yml"
            ansible.inventory_path = "playbooks/container-registry/inventory"
        end
    end
end
