$script = <<SCRIPT
SCRIPT
Vagrant.configure(2) do |config|
  config.vm.box = "generic/rhel7"
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |vbox|
    vbox.memory = 4096
    vbox.cpus = 2
    vbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vbox.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  config.vm.network "private_network", ip: "192.168.50.10"
  config.vm.hostname = "box"
  config.vm.define :box do |box| end
  config.vm.provision "shell", inline: $script
end