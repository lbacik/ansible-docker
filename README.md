# ansible-docker

You have to prepare your own `hosts` file (see hosts_example for a hint what/how/where ;) ).

## use case

Typical use can be like below:

copy your ssh key to the server:

	$ ssh-copy-id user@server

User `user` have to be added to /etc/sudoers file (or be in sudo group)!

	%sudo  ALL=(ALL:ALL) NOPASSWD: ALL

Add host(s) to `hosts` file:

	example ansible_host=server ansible_user=user

And run playbooks you want to!

## playbooks

To install docker on debian:

	$ ansible-playbook playbooks/docker/install-dockerd.yml

To configure docker api on port 2375 (systemd):

	$ ansible-playbook playbooks/docker/configure-systemd.yml

If you want to secure your api with certificates (port 2376, configure-systemd-tls.yml) you have to first generate certs and put them in `tsl` directory:

- docker.key
- docker.pem
- myCA.pem

