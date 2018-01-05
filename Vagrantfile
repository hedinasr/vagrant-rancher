nodes = [
  { :hostname => 'master1',  :ip => '172.16.66.2', :ram => 2048 },
  #{ :hostname => 'master2',  :ip => '172.16.66.3', :ram => 2048 },
  { :hostname => 'node1',  :ip => '172.16.66.4', :ram => 1024 },
  { :hostname => 'node2',  :ip => '172.16.66.5', :ram => 1024 },
  { :hostname => 'node3',  :ip => '172.16.66.6', :ram => 1024 },
  { :hostname => 'proxy1',  :ip => '172.16.66.7', :ram => 1024 }
]

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "bento/ubuntu-16.04";
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      memory = node[:ram] ? node[:ram] : 256;
      nodeconfig.vm.provider :libvirt do |libvirt|
        libvirt.storage :file, :size => '10G'
        libvirt.memory = memory.to_s
        libvirt.cpus = 1
        libvirt.graphics_type = "none"
      end
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    swapoff -a
  SHELL
end
