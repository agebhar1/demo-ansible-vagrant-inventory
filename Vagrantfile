# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

inventory = YAML.load_file('inventory/vagrant.yml')

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"

  inventory['all']['hosts'].each do |hostname, host_config|

    config.vm.define hostname do |node|

      node.vm.hostname = hostname
      node.vm.network :private_network, ip: host_config['ansible_host']
      node.vm.provider "virtualbox" do |vb|
      end

      vm = host_config.dig('vagrant', 'vm') || {}
      vm.each do |key, value|
        if key.start_with?('box')
          node.vm.send(key + '=', value)
        end
      end

    end

  end

end
