
Vagrant.require_version ">= 1.7.0"

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"
  master = 1
  node = 2
  # Set virtualbox func
  def set_vbox(vb, config)
    vb.gui = false
    vb.memory = 1536
    vb.cpus = 1

    config.vm.box = "rafacas/centos71-plain"
  end

  private_count = 10
  (1..(master + node)).each do |mid|
    name = (mid <= node) ? "node" : "master"
    id   = (mid <= node) ? mid : (mid - node)

    config.vm.define "#{name}#{id}" do |n|
      n.vm.hostname = "#{name}#{id}"
      ip_addr = "172.16.35.#{private_count}"
      n.vm.network :private_network, ip: "#{ip_addr}",  auto_config: true

      n.vm.provider :virtualbox do |vb, override|
        vb.name = "kube-#{n.vm.hostname}"
        set_vbox(vb, override)
      end
      private_count += 1
      
      config.vm.provision "shell", inline: "sudo swapoff -a", run: "always"
    end
  end
end
