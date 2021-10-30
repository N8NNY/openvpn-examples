pub_key = ENV["VAGRANT_PUB_KEY"]
Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.vm.network "public_network", bridge: 'enp3s0', dev: 'enp3s0'

  config.vm.define "openvpn" do |openvpn|
    openvpn.vm.hostname = "openvpn.local"
    openvpn.vm.provider :libvirt do |libvirt|
      libvirt.memory = 1024
      libvirt.cpus = 4
    end
  end

  (1..3).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.hostname = "node#{i}.local"
      node.vm.provider :libvirt do |libvirt|
        libvirt.memory = 2048
        libvirt.cpus = 2
      end
    end
  end

  config.vm.provision "shell",
  inline: "sudo apt-get update && sudo apt-get install avahi-daemon avahi-discover avahi-utils libnss-mdns mdns-scan -y"
  config.vm.provision "shell", inline: "echo '#{pub_key}' >> /home/vagrant/.ssh/authorized_keys", privileged: false
end
