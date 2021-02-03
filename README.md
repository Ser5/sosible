## Ubuntu

	apt update
	apt install software-properties-common
	apt-add-repository --yes --update ppa:ansible/ansible
	apt install ansible

## Debian

	echo -e "\ndeb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main\n" >> /etc/apt/sources.list
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
	apt update
	apt install ansible

## Config

	sed -i 's/^hash_behaviour\s*=\s*replace/hash_behaviour = merge/' /etc/ansible/ansible.cfg
