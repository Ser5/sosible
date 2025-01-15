## Ubuntu 22, Debian 11

```bash
gpg --list-keys
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/ansible-keyring.gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo echo -e "\ndeb [signed-by=/usr/share/keyrings/ansible-keyring.gpg] http://ppa.launchpad.net/ansible/ansible/ubuntu focal main\n" >> /etc/apt/sources.list.d/ansible.list
sudo apt update
sudo apt install ansible -y
```

## Ubuntu 20

```bash
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```

## Debian 10

```bash
sudo echo -e "\ndeb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main\n" >> /etc/apt/sources.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo apt update
sudo apt install ansible -y
```

## Config

```bash
cat /etc/ansible/ansible.cfg
sudo mkdir /etc/ansible/
sudo echo "127.0.0.1 ansible_connection=local" >> /etc/ansible/hosts
sudo echo -e "\n[defaults]\nhash_behaviour = merge" >> /etc/ansible/ansible.cfg
```

## Download

```bash
sudo apt install git
mkdir ansible && cd ansible/
git clone https://github.com/Ser5/sosible/
echo -e "- name: Run\n  hosts: localhost\n\n  roles:\n    - role: sosible\n" > site.yml
mkdir host_vars && touch host_vars/vars.yml
```

## Run

```bash
cp defaults/main.example.yml defaults/main.yml
echo $'#!/bin/bash\n\nansible-playbook site.yml --extra-vars=\'@host_vars/vars.yml\' $@' > run
chmod u+x run
./run --list-tags
./run --tags=basic,git
```
