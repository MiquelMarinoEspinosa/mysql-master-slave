Vagrant.configure("2") do |config|
  config.vm.define "mysql-master" do |mysql_master|
    mysql_master.vm.box = "debian/jessie64"
    mysql_master.vm.hostname = "mysql-master"
    mysql_master.vm.network 'private_network', ip: '172.21.99.4'
    config.vm.provider "virtualbox" do |vb|
            vb.memory = "1024"
    end

    config.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.extra_vars = {
          hostname: "mysql-master"
        }
        ansible.playbook = "etc/devel/vagrant/provision/ansible/playbooks/master/playbook.yml"
    end	
 end  
 config.vm.define "mysql-slave" do |mysql_slave|
    mysql_slave.vm.box = "debian/jessie64"
    mysql_slave.vm.hostname = "mysql-slave"
    mysql_slave.vm.network 'private_network', ip: '172.21.99.5'
    config.vm.provider "virtualbox" do |vb|
            vb.memory = "1024"
    end
    config.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.extra_vars = {
          hostname: "mysql-slave"
        }
        ansible.playbook = "etc/devel/vagrant/provision/ansible/playbooks/slave/playbook.yml"    
    end	
  end
end
