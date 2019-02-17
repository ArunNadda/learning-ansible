# ansible config and inventories lab

##### ansible config file locations and precedences
##### ansible config file default location and default parameters
##### ansible config file (ini format)

##### ansible inventory file locations and precedence
##### ansible inventory file default location
##### inventory file (ini format)


#### 01:

##### check hosts file and ansible.cfg file
```
ansible all -m ping
```
##### output ???
```
ansible all -m ping -u user1
```

##### use ansible using passwordless ssh
##### create ssh key for ctrl host using
```
ssh-keygen


copy ssh pub key to app01
ssh-copy-id user1@app01

ansible all -m ping
```
##### copy it to all other hosts under user1:
##### for i in `cat all_hosts`; do echo $i; ssh-copy-id user1@$i; done


---
#### 02:

modify ansible.cfg (without hostkey check)


ansible app -m ping
ansible all -m ping

---
03:

modify ansible.cfg (remote_user)

ansible app -m ping
ansible all -m ping


---
04:

hosts file
 -- groups
 -- members
 -- range in groups
 -- children

ansible prod -m ping
ansible all -m ping


host patterns:

ansible '*' -m ping
ansible centos -m ping

ansible all --list-hosts

---------
05 and 06:


inventories adv. (e.g. host vars, group vars...etc)

after adhoc commands:
