# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "precise32"
    config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    config.vm.network :forwarded_port, guest: 80, host: 3456  # nginx
    config.vm.network :forwarded_port, guest: 5432, host: 4567  # postgres
    config.vm.hostname = "dot"

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", 512]
    end

    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "cookbooks"
        chef.roles_path = "roles"
        chef.json  = {
            :user => "vagrant",
            :servername => "127.0.0.1",
            :dbname => "dot_database",
            # Comented for dev
            # :staticfiles => "/opt/dot/collected_static/",
            :postgresql => {
                :password => {
                    :postgres  => "123456"
                }
            },
            :users => [
                {
                    :name => "dot_user",
                    :key => "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDhmTcCTaEoRDM8CgDFL8iDLUUhdGy7kFeNI0U7N+T7Rp/3ovcVPWWjviH5Hzk6HvxAH9sfZ1X11AGupi2YPQGXnJzqUXD092LbBq/ZcJDg4E0ZzvQCIW0kSKbCAQg/rXhJB07Ew4+c4NblyvCEtIw0MoSG1r/wOa5Z2UlMQMYdopu/rRxTsVhgL77kk+1lOWc816CB6HQHEcMcABo7Kd+TCwCtjuzzY9tQWwQuI4Fj3Bq7PJwBUs8mA0vWbn/zoP/GU5CZha/pcpM6+IKDXAEdwf1ipOA3vlxugAmzytJR76UobjkJ4HMf72uEClsUmsdRYbyG4JCpNEqIabrmwMuR akiokio@Guilhermes-MacBook-Pro.local"
                }
            ]
        }
        chef.add_role "dot_user"
    end
end
