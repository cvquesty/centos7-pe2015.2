# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Define the Puppet Enterprise Version
  pe_version = '2015.2.0'
  config.pe_build.version       = pe_version
  config.pe_build.download_root	= "https://s3.amazonaws.com/pe-builds/released/#{pe_version}"

  # Define the Vagrant Box to Download
  config.vm.box = "puppetlabs/centos-7.0-64-nocm"

######################
## Puppet Master VM ##
######################
  # Define the Master VM Characteristics
  config.vm.define 'master' do |master|
    master.vm.network :private_network, :ip => '10.10.100.100'
    master.vm.network "forwarded_port", guest: 443, host: 8443
    master.vm.hostname = 'master.puppetlabs.vm'

  # Configure Master VM Settings
  master.vm.provider :virtualbox do |settings|
    settings.memory = 4096
    settings.name = "c7master_2015.2.0"
    settings.cpus = 2
  end

  # Add all other hosts for environment
  master.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm', 'master']
    entries.add_host '10.10.100.111', ['development.puppetlabs.vm', 'development']
    entries.add_host '10.10.100.112', ['testing.puppetlabs.vm', 'testing']
    entries.add_host '10.10.100.113', ['production.puppetlabs.vm', 'production']
  end

  # Set the PE Role for this node
  master.vm.provision :pe_bootstrap do |provisioner|
    provisioner.role = :master
  end
    master.vm.provision :shell, path: "provision/master.sh"
  end

###################
## Develpment VM ##
###################
  # Define the Development VM Characteristics
  config.vm.define 'development' do |development|
    development.vm.network :private_network, :ip => '10.10.100.111'
    development.vm.hostname = 'development.puppetlabs.vm'

  # Configure Development VM Settings
  development.vm.provider :virtualbox do |settings|
    settings.memory = 512
    settings.name = "c7development_2015.2.0"
    settings.cpus = 1
  end

  # Add All Hosts for Environment
  development.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm', 'master']
    entries.add_host '10.10.100.111', ['development.puppetlabs.vm', 'development']
    entries.add_host '10.10.100.112', ['testing.puppetlabs.vm', 'testing']
    entries.add_host '10.10.100.113', ['production.puppetlabs.vm', 'production']
  end

  # Set the PE Role of This Node
  development.vm.provision :pe_bootstrap do |provisioner|
    provisioner.role = :agent
    provisioner.master = 'master.puppetlabs.vm'
  end
    development.vm.provision :shell, path: "provision/development.sh"
  end

################
## Testing VM ##
################
  # Define the Testing VM Characteristics
  config.vm.define 'testing' do |testing|
    testing.vm.network :private_network, :ip => '10.10.100.112'
    testing.vm.hostname = 'testing.puppetlabs.vm'

  # Configure Testing VM Settings
  testing.vm.provider :virtualbox do |settings|
    settings.memory = 512
    settings.name = "c7testing_2015.2.0"
    settings.cpus = 1
  end

  # Add All Hosts for Environment
  testing.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm', 'master']
    entries.add_host '10.10.100.111', ['development.puppetlabs.vm', 'development']
    entries.add_host '10.10.100.112', ['testing.puppetlabs.vm', 'testing']
    entries.add_host '10.10.100.113', ['production.puppetlabs.vm', 'production']
  end

  # Set the PE Role of This Node
  testing.vm.provision :pe_bootstrap do |provisioner|
    provisioner.role = :agent
    provisioner.master = 'master.puppetlabs.vm'
  end
    testing.vm.provision :shell, path: "provision/testing.sh"
  end

###################
## Production VM ##
###################
  # Define the Production VM Characteristics
  config.vm.define 'production' do |production|
    production.vm.network :private_network, :ip => '10.10.100.113'
    production.vm.hostname = 'production.puppetlabs.vm'

  # Configure Production VM Settings
  production.vm.provider :virtualbox do |settings|
    settings.memory = 512
    settings.name = "c7production_2015.2.0"
    settings.cpus = 1
  end

  # Add All Hosts for Environment
  production.vm.provision :hosts do |entries|
    entries.add_host '10.10.100.100', ['master.puppetlabs.vm', 'master']
    entries.add_host '10.10.100.111', ['development.puppetlabs.vm', 'development']
    entries.add_host '10.10.100.112', ['testing.puppetlabs.vm', 'testing']
    entries.add_host '10.10.100.113', ['production.puppetlabs.vm', 'production']
  end

  # Set the PE Role of This Node
  production.vm.provision :pe_bootstrap do |provisioner|
    provisioner.role = :agent
    provisioner.master = 'master.puppetlabs.vm'
  end
    production.vm.provision :shell, path: "provision/production.sh"
  end
end
