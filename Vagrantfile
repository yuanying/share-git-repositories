# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
GIT_PROJECT_ROOT = ENV["GIT_PROJECT_ROOT"]
GIT_HOST_PORT = ENV["GIT_HOST_PORT"].to_i | 9090
raise "Set GIT_PROJECT_ROOT" unless GIT_PROJECT_ROOT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 8080, host: GIT_HOST_PORT

  config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder GIT_PROJECT_ROOT, "/repositories", mount_options: ['dmode=777','fmode=755']

  config.vm.provision "shell", inline: <<-EOT
    apt-get update
    apt-get install -y git-core
    gem install bundler
    if [ ! -d /vagrant/grack ]
    then
        git clone https://github.com/schacon/grack.git /vagrant/grack
        su - vagrant -c 'cd /vagrant/grack; bundle install'
    fi
    cp /vagrant/config.ru /vagrant/grack/config.ru
    cp /vagrant/grack.conf /etc/init/grack.conf
    service grack start
  EOT
end
