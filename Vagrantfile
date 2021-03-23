
Vagrant.configure("2") do |config|

  diskStorage = './ubuntuHDD.vdi'
  
  config.vm.box = "generic/ubuntu2004"
  config.vm.network "private_network", ip: "192.168.10.77"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "2048"
    
    unless File.exist?(diskStorage)
      vb.customize ['createhd', '--filename', diskStorage, '--variant', 'Fixed', '--size', 12 * 1024] 
    end

    vb.customize ['storageattach', :id, '--storagectl', 'IDE Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', diskStorage] 
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.verbose = 'v'
    ansible.playbook = 'main.yml'       
  end
  
end
