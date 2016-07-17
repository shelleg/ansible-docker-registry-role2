# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    ansible_verbosity='-v'
    machines = [
      {
        :name => "ubuntu1604",
        :box => "bento/ubuntu-16.04",
        :ip => "192.168.50.3"
      },
      {
        :name => "ubuntu1404",
        :box => "ubuntu/trusty64",
        :ip => "192.168.50.2"
      }
    ]

    machines.each do |opts|

      config.vm.define opts[:name] do |machine|
        machine.vm.network "private_network", ip: opts[:ip]
        machine.vm.hostname = opts[:name]
        machine.vm.box = opts[:box]
        machine.vm.provision :ansible do |ansible|
            ansible.limit = opts[:name]
            ansible.playbook = "./playbook.yml"
            ansible.sudo = "true"
            ansible.sudo_user = "root"
            ansible.host_key_checking = "false"
            ansible.verbose = "#{ansible_verbosity}"
            ansible.extra_vars = {
               hosts: "/usr/local/etc/ansible/hosts",
               #dict: {
               #  key1: "val1",
               #  key2: "val2"
               #}
             }
        end
      end
    end
end

