Vagrant.configure("2") do |config|
  # general configuration
  config.vm.box = "debian/bookworm64"
  config.vagrant.plugins = "vagrant-libvirt"

  # load SSH-Public-Key
  ssh_key_path = File.expand_path("~/.ssh/id_ed25519.pub")
  ssh_pub_key = File.read(ssh_key_path) if File.exist?(ssh_key_path)

  # machine configuration
  machines = [
    { name: "server",  ip: "192.168.56.10" },
    { name: "node-0",  ip: "192.168.56.11" },
    { name: "node-1",  ip: "192.168.56.12" }
  ]

  machines.each do |machine|
    config.vm.define machine[:name] do |node|
      node.vm.hostname = machine[:name]
      node.vm.network "private_network", ip: machine[:ip], libvirt__network_name: "default"

      node.vm.provider "libvirt" do |libvirt|
        libvirt.memory = 2048
        libvirt.cpus = 1
        libvirt.storage :file, :size => '20G'
      end

      # add SSH Key
      if ssh_pub_key
        node.vm.provision "shell", inline: <<-SHELL
          mkdir -p /home/vagrant/.ssh
          echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
          chown -R vagrant:vagrant /home/vagrant/.ssh
          chmod 600 /home/vagrant/.ssh/authorized_keys
        SHELL
      end
    end
  end
end
