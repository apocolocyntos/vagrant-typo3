Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"
  config.vm.box_check_update = true
  config.vm.hostname = "typo3"
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
   config.vm.network "private_network", ip: "192.168.56.10"
  #config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = "2"
    vb.name = "typo3-stack"
  end
  config.vm.provision "file", source: "./typo3.yml", destination: "/home/vagrant/typo3.yml"
  config.vm.provision "file", source: "./composer.json", destination: "/home/vagrant/composer.json"
  config.vm.provision "file", source: "./99-typo3.ini", destination: "/home/vagrant/99-typo3.ini"
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y ansible aptitude
    ansible-playbook /home/vagrant/typo3.yml
  SHELL
end
