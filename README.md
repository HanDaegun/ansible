Ansible
====

## Environment

macOS High Sierra バージョン 10.13.2での環境構築

### Vagrant

Vagrantbox.es (http://www.vagrantbox.es/) からお目当てのCentOS7を探してbox追加

```bash
$ vagrant box add Centos72 https://github.com/CommanderK5/packer-centos-template/releases/download/0.7.2/vagrant-centos-7.2.box
$ mkdir -p ~/work/boxes/data
$ mkdir -p ~/work/boxes/centos72
$ cd ~/work/boxes/centos72
$ vagrant init
$ vi Vagrant

# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "centos72"
  config.vm.define "dev1" do |atomic|
    atomic.vm.network "forwarded_port", guest: 22, host: 2222
    atomic.vm.network "private_network", ip: "192.168.33.10"
    atomic.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
    atomic.vm.synced_folder "../data", "/vagrant_data"
  end
end

$ vagrant up
$ vagrant ssh
```
