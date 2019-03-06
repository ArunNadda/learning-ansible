## 03-Ansible-as-AdHoc-Tool
## ------------------------

### AdHoc commands and modules

### command modules

###### can run adHoc commands from control node to any number of nodes
###### It is default module

```
# ansible all -m command -a uptime
# ansible all -a uptime
```
###### running command one host at a time (fork 1)

```
# ansible all -f 1 -a "free"
```
##### practice adHoc commands (command module by default is not idempotent)
##### use creates and removes for idempotency
##### check documentation

```
Run below command:
ansible app -s -a "useradd user2"

run again:

ansible app -s -a "useradd user2"


-- Some commands are IDEMPOTENT by design though,

-- install vim on app group

ansible app -a "yum install -y vim"
ansible app -s -a "yum install -y vim"
```


##### more examples
```
-- command module (default)

get hostnames
get uptime

ansible all -m command -a uptime

ansible all -a uptime
ansible all -a uptime -o
ansible all -a free


running one system at at time:
ansible all -f 1 -a "free"

ansible app -s -a "useradd user2"
run again:

ansible app -s -a "useradd user2"
ansible app -s -a "userdel user2"

** idempotency ** ??

-- install vim on app group

ansible app -a "yum install -y vim"

ansible app -s -a "yum install -y vim"

```


### setup module
#### used to gather facts, when executing playbook

```
ansible app01 -m setup

```
###### grep for ip, ansible_distribution etc


### Using modules (AdHoc):

##### file module
##### copy module
##### group module

##### create group:
```
ansible prod -s -m group -a "name=ansible state=present"
ansible prod -b -m group -a "name=ansible state=present"
ansible prod -b -m group -a "name=ansible state=present gid=1001"
```

##### user module
##### create user: (with uid??)
```
ansible app -b -m user -a "name=ansible group=ansible createhome=yes"
ansible prod -b -m user -a "name=ansible group=ansible createhome=yes"
```
##### for practice (and use ansible from next session on)
##### provide sudo access to ansible user:



### more practice:

##### copy module
##### command module
##### shell module
##### raw module
##### copy local file to remote nodes
##### copy remote file to remote node
#####  check module documentation


#####  check source code of say copy module (.py file)
```
ansible-doc copy
```
