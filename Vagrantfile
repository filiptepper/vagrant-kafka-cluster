Vagrant.configure("2") do |config|
  config.vm.box              = "ubuntu/trusty64"
  config.vm.box_check_update = false

  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.memory                = 1024
    virtualbox.check_guest_additions = false
    virtualbox.functional_vboxsf     = false
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  1.upto(3).each do |i|
    config.vm.define "kafka-#{i}" do |host|
      host.vm.network "private_network",
        ip: "192.168.39.3#{i}"

    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "zookeeper.yml"
  end if ENV['ZOOKEEPER'] == '1'

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "kafka.yml"
  end if ENV['KAFKA'] == '1'
end
