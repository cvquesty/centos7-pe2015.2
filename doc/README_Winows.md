#Windows Installation Instructions

##Install Software

Install Vagrant
https://dl.bintray.com/mitchellh/vagrant/vagrant_1.7.2.msi

Install Virtualbox
http://download.virtualbox.org/virtualbox/4.3.20/VirtualBox-4.3.20-96997-Win.exe

Install Mysysgit
https://github.com/msysgit/msysgit/releases/download/Git-1.9.5-preview20141217/Git-1.9.5-preview20141217.exe

Atom
https://atom.io/download/windows

##Install Plugins and Download PE

    vagrant plugin install vagrant-hosts
    vagrant plugin install vagrant-pe_build

Due to the way vagrant-pe_build handles temp files you will need to download the PE tar ball.

Download Puppet Package
https://s3.amazonaws.com/pe-builds/released/3.7.1/puppet-enterprise-3.7.1-el-6-x86_64.tar.gz

Move it to the C:\Users\<username>\.vagrant.d\.pe_builds directory.

Turn off windows firewall.

##Launch Vagrant instances

    cd vagrant-ss
    vagrant up

##Notes:

* This environment requires your machine to have at least 8GB of RAM.
* This has been tested to work in Windows 8.1.
