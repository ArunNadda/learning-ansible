# ansible config and inventories lab

##### ansible config file locations and precedences
##### ansible config file default location and default parameters
##### ansible config file (ini format)

##### ansible inventory file locations and precedence
##### ansible inventory file default location
##### inventory file (ini format)


#### 01:

##### login as ansible user

##### check hosts file and ansible.cfg file

###### run below command to check if hosts in inventory file are reachable

```
ansible all -m ping
```
##### output ???
```
ansible all -m ping -u user1
```
##### output ???
```

ansible all -m ping -u user1 --ask-pass

```

##### use ansible using passwordless ssh
##### create ssh key for ctrl host using

```
ssh-keygen


copy ssh pub key to app01
ssh-copy-id user1@app01

ansible all -m ping

ansible all -m ping -u user1

```
##### copy it to all other hosts under user1:
##### for i in `cat all_hosts`; do echo $i; ssh-copy-id user1@$i; done


---
#### 02:

##### remove host detail from known_hosts in ctrl node

##### modify ansible.cfg (no hostkey check)

```
ansible app -m ping -u user1
ansible all -m ping -u user1
```
---
#### 03:

##### modify hosts (add ansible_connection)

```
ansible app -m ping -u user1
ansible all -m ping -u user1
```
---
#### 04:

##### modify ansible.cfg (add remote_user)

```
ansible app -m ping
ansible all -m ping
```

---
#### 05:

##### modify hosts file to add all hosts
#####  -- groups
#####  -- members
#####  -- range in groups
#####  -- children



```
ansible all --list-hosts


ansible prod -m ping
ansible all -m ping
```
##### *** introduce retry file location


##### host patterns:
```
ansible '*' -m ping
ansible centos -m ping
```
---
#### 06:

##### modify app02 for ssh port 2222
##### modify inventory to reflect it on app02
#####

```
ansible app -m ping
ansible all -m ping
```

---
#### 07 (host vars):

##### modify inventory to reflect it on app02
##### create new user on app03
##### add to inventory

```
ansible app -m ping
ansible all -m ping
```

---
#### 08 (group vars):

##### modify inventory to add prod group vars


```
ansible prod -m ping
ansible all -m ping
```

---
#### 09 (all vars):

##### modify inventory to add all vars


```
ansible all -m ping
```

---------
#### 10:
##### discuss host patterns

##### Host patterns (in ansible command)
##### [all] check the error
##### [all:vars]


```
ansible all -a "id -a" 

Wildcards (‘*’, all, ‘app*’, ‘*.test.com’)
Hosts/groups (app01, app01:app02, db, app:lb)
Subscripts (app[0], prod[0:3])
Exclusion (!db, ‘prod:!db’)
Intersection (&, ‘prod:&app’)
Regex (‘~(app|db).*’)
```
##### In addition to hosts patterns, --limit option can be used to restrict execution to specific set of hosts or groups.


##### inventories adv. (e.g. host vars, group vars...etc)
