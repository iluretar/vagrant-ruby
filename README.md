# Vagrant Ruby

Vagrant Vm for ruby on rails development.

## Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant](http://vagrantup.com)

## Plugins

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-librarian-chef-nochef
```

## Initial Setup

```bash
vagrant up
cd /vagrant/
gem install bundler
rbenv rehash
```
