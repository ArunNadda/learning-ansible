module02 - 02 Ansible-AdHoc
----------------------------

AdHoc commands and modules
----------------------------

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


Using modules (AdHoc):


create group:
ansible all -s -m group -a "name=ansible state=present"
ansible all -b -m group -a "name=ansible state=present"
ansible all -b -m group -a "name=ansible state=present gid=1001"


create user: (with uid??)
ansible all -b -m user -a "name=ansible group=ansible createhome=yes"

*** how will it behave?

ansible all -b -m user -a "name=ansible group=ansible createhome=yes"

**** for practice (and use ansible from next session on)
provide sudo access to ansible user:



use:

copy module
command module
shell module
