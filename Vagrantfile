# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  pref = YAML.load_file("config.yaml")
  if !pref.has_key?('32bit') or !pref.has_key?('memory')
    abort("Your config.yaml must specify a '32bit' and 'memory' setting.")
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = pref['proxyhttp']
    config.proxy.https    = pref['proxyhttps']
    config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  end

  config.vm.box = "jlintag/archlinux64base"
  #config.vm.network :private_network, ip: "192.168.68.8"

  config.vm.provider :virtualbox do |vb|
    vb.name = "developmentBox"
    vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", pref["memory"]]
  end

  config.vm.provision "shell", path: "plasma.sh"
end

