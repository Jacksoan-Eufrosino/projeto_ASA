Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  #A versao do Guest Additions dessa box é a 6.0, ja a do meu virtualbox
  #é a versao 7.1, logo estava gerando incompatibilidade. Foi necessario a
  #instalacao de um plugin para realizar o gerenciamento da guest additions
  # => vagrant plugin install vagrant-vbguest
  #e em seguida adicionar a linha abaixo.
  config.vbguest.auto_update = false

  config.vm.provision :ansible do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "playbook.yml"
  end

  config.vm.define "p01_jacksoan_gabriel" do |aluno|
    aluno.vm.hostname = "p01-jacksoan-gabriel"
    aluno.vm.network "private_network", ip: "192.168.57.10"

    aluno.vm.provider "virtualbox" do |vb|
      vb.name = "p01_jacksoan_gabriel"
      vb.memory = 1024
    end

    (0..2).each do |i|
      aluno.vm.disk :disk, size: "10GB", name: "disk-#{i}"
    end
  end
end
