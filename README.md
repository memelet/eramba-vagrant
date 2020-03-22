# Configure the Host Instance

## Install VirtualBox
As per https://www.virtualbox.org/wiki/Downloads

## Install Vagrant
As per https://www.vagrantup.com/docs/installation/

## Intall Vagrant plugins
```
vagrant plugin install vagrant-env
vagrant plugin install vagrant-hostmanager
```

## Install Python virtualenv
#### Mac OS
```
sudo easy_install pip
sudo pip install --upgrade pip
pip install virtualenv
```

#### Ubuntu/Debian
```
sudo apt install python-virtualenv
```

## Set up Python virtualenv for Ansible
```
mkdir .venvs
virtualenv .venvs/ansible-2.8
source .venvs/ansible-2.8/bin/activate
```

## Install Ansible

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

*TODO There are probably other host packages that need to be installed*
```
pip install 'ansible==2.8'
```

# Provision Eramba

## Checkout the eramba-vagrant project
```
git clone git@github.com:memelet/eramba-vagrant.git
cd eramba-vagrant
ansible-galaxy install --ignore-errors -r requirements.yml
```

## Create myslq backup directory
This directory will be mounted in the VM to be used as the target for eramba db backups.
```
mkdir -p .data/backups
```

## Install ansible roles
```
ansible-galaxy install -r requirements.yml
```

## Configure variables

Adjust the variables in `.env` as needed.

## Create the eramba instance

```
vagrant up
```

## Open eramba
At http://eramba

(Replace "eramba" with `VAGRANT_HOSTNAME` in .env if changed)

## Setup eramba

As per https://docs.google.com/document/d/1agWTzlJ965N0f-F6dqGxCHsQMaLXa2m1GhCDX1pqXHs

