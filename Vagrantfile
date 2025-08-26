Vagrant.configure("2") do |config|
    config.vm.box = "debian/bookworm64"
    config.vm.hostname = "carlyni1.lucas2" #adicionado o nome conforme o projeto específica
    config.ssh.insert_key = false
    if Vagrant.has_plugin?("vagrant-vbguest") #adicionado apenas por questão
        config.vbguest.auto_update = false #possível problema na máquina do laboratório
    end
    config.vm.network "private_network", ip: "192.168.56.137" # ajustando para o último dígito Carliny e Lucas
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.check_guest_additions = false # desabilita verificação de guest additions
    end
    config.vm.provision "ansible_local" do |ansible|
        #ansible.install = true 
        ansible.playbook = "playbook_ansible.yml" #ajustado para chamar o playbook diretamente
    end 
    
end
# feita identação do arquivo