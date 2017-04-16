# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
	{ :hostname => 'saltmaster', :ip => '192.168.99.131', :memory => 2048, :cpu => 1, :boxname => "ubuntu/trusty64" },
        { :hostname => 'saltminion', :ip => '192.168.99.132', :memory => 2048, :cpu => 1, :boxname => "ubuntu/trusty64" },
]


Vagrant.configure("2") do |config|
  nodes.each do |node|
      config.vm.box_check_update = false
      config.vm.define node[:hostname] do |nodeconfig|
          nodeconfig.vm.box = node[:boxname]
          nodeconfig.vm.hostname = node[:hostname]
	  nodeconfig.vm.network :private_network, ip: node[:ip]
          nodeconfig.vm.provider :virtualbox do |vb|
            vb.memory = node[:memory]
            vb.cpus = node[:cpu]
          end
        end
  end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "salt.yml"
  end
  

end
