# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.name = "ruby-devbox"
  end

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.hostname = "ruby-devbox"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "nodejs"
    chef.add_recipe "build-essential::default"
    chef.add_recipe "ruby_build"
    chef.add_recipe "rbenv::user"
    chef.add_recipe "rbenv::vagrant"
    chef.add_recipe 'postgresql::server'
    chef.add_recipe 'postgresql::libpq'

    chef.json = {
      rbenv: {
        user_installs: [{
          user: 'vagrant',
          rubies: ["2.2.1"],
          global: "2.2.1",
          gems: {
            "2.2.1" => [{
              name:"bundler"
              }]
          }
        }]
      },
      postgresql: {
        version:"9.3",
        port:"5432",
        listen_addresses:"*",
        pg_hba: [
          {
            type: "host",
            db: "all",
            user: "vagrant",
            addr: "127.0.0.1/32",
            method: "trust" }
        ],
        users: [
          {
            username: "vagrant",
            password: "",
            superuser: true,
            replication: false,
            createdb: true,
            createrole: false,
            inherit: true,
            replication: false,
            login: true
          }
        ]
      }
    }
  end
end
