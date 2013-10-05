Vagrant - Varnish
=========================

Vagrant machine with Varnish installed. I needed to test something with the following scenario:
- web server installed locally (osx)
- varnish

Initially I've setup everything on my box, but that tends to cover up some potential issues. 
So ideally, I wanted Varnish to be in an environment setup closer to production (separate server). 
I searched for other vagrant setups with Chef, but they have also a web server (nginx/apache), 
php, mysql and so on installed on the same machine.

I am using Vagrant 1.3.2 and Chef Solo for provisioning.
### Installation

```
git clone https://github.com/florinel-chis/vagrant-varnish-chef_solo.git
git submodule init
git submodule update
```

### How to use it
```
cd vagrant-varnish-chef_solo
vagrant up
vagrant provision
```
then open [http://192.168.10.10/](http://192.168.10.10/) in your browser. This ip address is the one specified in `Vagrantfile`: `config.vm.network :private_network, ip: "192.168.10.10"`

### Vagrantfile
In my case I use the following configuration: the web server installed on my local machine is listening to `80`and my ip address is `192.168.0.8`
```
 chef.json = {
      :varnish => {
        :listen_port => 80,
        :backend_host => '192.168.0.8',
        :backend_port => 80,
      }
    }
```

You can adjust it with your settings. To check what settings are used by Varnish:

```
vagrant ssh
cat /etc/varnish/default.vcl
```


