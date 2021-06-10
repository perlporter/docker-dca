# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "master"   => {"memory" => "2048", "cpu" => "2", "ip" => "100", "image" => "hashicorp/bionic64"},
  "node01"   => {"memory" => "1024", "cpu" => "2", "ip" => "110", "image" => "hashicorp/bionic64"},
  "node02"   => {"memory" => "1024", "cpu" => "2", "ip" => "120", "image" => "centos/7"},
  "registry" => {"memory" => "2048", "cpu" => "2", "ip" => "200", "image" => "hashicorp/bionic64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.docker-dca.example"
      machine.vm.network "public_network", ip: "10.20.20.#{conf["ip"]}"
      machine.vm.provider "vmware_desktop" do |vmware|
    #    vmware.name = "#{name}"
        vmware.memory = conf["memory"]
        vmware.cpus = conf["cpu"]
    #    vmware.customize ["modifyvm", :id, "--groups", "/Docker-DCA"]
      end
      machine.vm.provision "shell", path: "provision.sh"
    end
  end
end
