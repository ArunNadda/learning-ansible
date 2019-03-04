## session-01 Recheck:
## ===================

#### -- check if session-01 changes are present?
#### -- to make all changes consistent, docker instances should be shutdown using docker-compose stop every time

```
# cd /root/learning-ansible/akn/
# docker-compose stop
```


### How to bring it lab to status where it was left at last session.

#### login to control node:

```
docker exec -it akn_ctrl_1 /bin/bash

cd /workspace
```
##### check if its still owned by ansible:ansbile and cloned repo is still present), if not change ownership of /workspace to ansible:ansible ##### and clone git using ansible user

```
# chown ansible:ansible /workspace
# su - ansible
# git clone https://github.com/ArunNadda/learning-ansible.git
# cd /workspace/learning-ansible/ansible_sessions/session-01/02-Ansible-inventories/
```
#### configure passwordless ssh from ctrl node to all other nodes:

```
# ssh-key-gen
# for i in `cat all_hosts`; do echo $i; ssh-copy-id user1@$i;done
```
#### check if all hosts are reachable from ansible ctrl nodes

```
# cd rev07
# ansible all -m ping
```

#### check app02 is running sshd on port 2222, if not configure it to run on 2222

#### homework:
#### create ansible user and ansible group on host app03 with sudo access.



#### Some more commands to try

```
ansible all --list-hosts
ansible all -a 'id -a'
ansible '*' -m ping
ansible 'all:!app01:!lb01' -m ping
ansible 'all:!app' -m ping
ansible all -m ping --limit=app01
ansible all -m ping --limit=app
```
