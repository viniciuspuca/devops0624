Vagrant.configure("2") do |config|
# PROVISIONING PARA RODAR SCRIPT
  config.vm.provision "shell", path: "script.sh"
# VM CONTROLE
  config.vm.define "controle" do |controle|
    controle.vm.box = "shekeriev/debian-11"
    controle.vm.hostname = "controle"
    controle.vm.network "private_network", ip: "192.168.57.100"
    controle.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "1048"
      vb.cpus = 2
      vb.name = "controle"
    end
    controle.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.install_mode = "pip"
    end
    controle.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "installdocker.yml"
      ansible.install_mode = "pip"
    end

  end
# VM WEB SERVER
  config.vm.define "web" do |web|
    web.vm.box = "shekeriev/debian-11"
    web.vm.hostname = "web"
    web.vm.network "private_network", ip: "192.168.57.101"
    web.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
      vb.cpus = 2
      vb.name = "web"
    end
  end
# VM DATABASE
  config.vm.define "db" do |db|
    db.vm.box = "shekeriev/debian-11"
    db.vm.hostname = "db"
    db.vm.network "private_network", ip: "192.168.57.102"
    db.disksize.size = '20GB' #AUMENTAR O ESPAÇO EM DISCO
    db.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
      vb.cpus = 2
      vb.name = "db"
    end
  end
# LOOP PARA CRIAR VMs SEMELHANTES
#  (1..3).each do |i|
#    config.vm.define "vm#{i}" do |node|
#      node.vm.hostname = "node#{i}"
#      node.vm.box = "shekeriev/debian-11"
#      node.vm.network "private_network", ip: "192.168.57.#{10 + i}"
#      node.vm.provider "virtualbox" do |vb|
#        vb.name = "vm#{i}"
#        vb.memory = "512"
#        vb.cpus = 2
#      end
#    end
#  end
end
