Vagrant.configure("2") do |config|

  config.vm.box = "precise64"
  
  #this should be enough, no port fw needed
  config.vm.network :private_network, ip: "192.168.10.10"
  
  #config.vm.network :forwarded_port, guest: 80, host: 4567

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe("apt")
    chef.add_recipe("varnish")
    chef.add_recipe("git")
    chef.add_recipe('zsh')

    chef.json = {
      :varnish => {
        :listen_port => 80,
        :backend_host => '192.168.0.8',
        :backend_port => 80,
      }
    }

  end

end
