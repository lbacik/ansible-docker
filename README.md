# ansible-docker


## ssh

Ansible requires ssh to work, so if it still needs to be done, you have to configure ssh with the publickey authentication on the remote server.

	$ ssh-copy-id user@server

User `user` have to be added to /etc/sudoers file (or be in sudo group)!

	%sudo  ALL=(ALL:ALL) NOPASSWD: ALL

## configuration

Prepare your own `hosts`:

```
cp hosts_example hosts
```



## playbooks

To install docker on debian:

	$ ansible-playbook playbooks/docker/install-dockerd.yml

To add configured user to `docker` group (if required):

```
$ ansible-playbook playbooks/docker/user-mod.yml
```



### Remote docker via docker api

Nowadays, the preferred way to access the remote docker instance is through the ssh protocol (at least to me); however, if, for some reason, you want to expose the docker api on the remote host, you can use the `configure-systemd` playbook for that.

To configure docker api on port 2375 (systemd):

	$ ansible-playbook playbooks/docker/configure-systemd.yml

If you want to secure your api with certificates (port 2376, configure-systemd-tls.yml) you have to first generate certs and put them in `tsl` directory:

- docker.key
- docker.pem
- myCA.pem

