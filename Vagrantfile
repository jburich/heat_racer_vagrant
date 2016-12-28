# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define "ng.hr" do |nghr|
    nghr.vm.box = "centos/7"
    nghr.vm.hostname = "ng.hr"
    nghr.vm.network :private_network, ip: "10.225.0.110"
    nghr.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "ng.hr"]
    end
    nghr.vm.synced_folder "../heat_racer_website", "/var/www/html/ng"
  end
  config.vm.define "couchbase.hr" do |couchbase|
    couchbase.vm.box = "centos/7"
    couchbase.vm.hostname = "couchbase.hr"
    couchbase.vm.network :private_network, ip: "10.225.0.130"
    couchbase.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "couchbase.hr"]
    end
  end
  config.vm.define "syncgw.hr" do |syncgw|
    syncgw.vm.box = "centos/7"
    syncgw.vm.hostname = "syncgw.hr"
    syncgw.vm.network :private_network, ip: "10.225.0.120"
    config.vm.network "forwarded_port", guest: 4984, host: 4984
    syncgw.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "syncgw.hr"]
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/configure.yml"
    ansible.inventory_path = "ansible/inventory"
  end
end
