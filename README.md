# Provision a LAMP stack on CentOS 7 server with Ansible
This playbook first provisions and locks down a new CentOS 7 hosts, then install
a secure LAMP stack on a cluster of servers.

## Requirements

Run this command to install dependencies under ./required-roles

`ansible-galaxy install -r requirements.yml`

## Roles & Tasks

### Dependencies
* [ansible-centos7-common](https://github.com/hongboni/ansible-centos7-common)

### LAMP play
* Secure hosts via above common playbook
* Install and configure a secure MariaDB server
* Install and configure HTTPD with PHP

## Example Plays

Run the 'LAMP' playbook against a list of hosts as defined in file ./hosts

Before running the next script, you need to make sure that you can log into the remote host
as the root user without password using ssh keys.


```
ansible-playbook site.yml 
```

If you have previously secured all the hosts via 
[ansible-secure-centos7](https://github.com/hongboni/ansible-secure-centos7) playbook,
then you can just run the LAMP playbook

```
ansible-playbook lamp.yml 
```


After running site.yml script, you can only log into the remote host via sudo user '*centos*'.
Current host can still access remote host via port 22, 

```
ssh centos@remote.host.ip
```

All other machines can only access the remote hosts via a special port of 22022 
(as defined in ansible-centos7-common role).

```
ssh -p 22022 centos@remote.host.ip
```

## License
BSD
