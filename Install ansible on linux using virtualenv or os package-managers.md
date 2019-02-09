# Installing ansible on Linux (CentOS/RHEL/Ubuntu) systems:
#

## About Ansible:
###### Ansible is an open source configuration management tool, and it supports managing the configurations of Unix-like and Microsoft Windows systems. Ansible manages nodes over SSH or PowerShell and python must be installed on them.
###### Ansible helps to perform configuration management and deployment of softwares on 100s of nodes using SSH, the entire operation can be executed by one single command of ansible. 

##### This article shall help to install Ansible on CentOS 7 / Ubuntu 18.04 / Ubuntu 16.04 / Debian 9.

## Architecture
###### Other configuration management tools like puppet, chef etc server software is installed on one machine, and client machines are managed through the agent. Wherein Ansible, the nodes are managed by controlling machine (Ansible server) over SSH, so there is no need to install agent on "client" machines.
###### Ansible deploys modules to nodes over SSH. Modules are nothing, but a script written in any language such as Python, Perl, Ruby, bash etc.

## System Requirements

## Controlling Machine
###### Ansible can run on any machine which has Python 2.6 or 2.7 installed.
###### Supports Red Hat, Debian, CentOS, OS X, any of the BSDs.

## Client Nodes
###### Client machines should at least have Python 2 (version 2.6 or later) or Python 3 (version 3.5 or later)
###### If you have SELinux enabled on remote nodes, you will have to install libselinux-python package on nodes before using any copy/file/template related functions in Ansible

## Install Ansible on CentOS 7 / RHEL 7 / Ubuntu 18.04 / 16.04 & Debian 9


### Paths to install Ansible on different OS:
###### We will discuss two main methods to install Ansible on Linux
###### 1. using virtualenv and pip
###### 2. using OS package-managers


#### 1. Step to install Ansible using virtualenv and pip

##### Install virtualenv:

###### RHEL/CentOS 7
###### On RHEL/CentOS, you can install by using yum.
```
sudo yum install python-virtualenv
```

###### Ubuntu/Debian
###### On Ubuntu/Debian, you can install by using apt.
```
sudo apt install python-virtualenv
```

#### Set up virtualenv:

###### After virtualenv installation, you can create a "virtual environment" to host local copy of Ansible.

```
# virtualenv myansible
```

###### This command creates a directory called myansible in  current working directory, it contains a copy of Python that will install modules in the myansible directory. This keeps them separate from other modules.
###### To use this new location, it must be activated.

```
# source myansible/bin/activate
```

###### prompt changs to include the virtualenv name. For example:

```
(myansible) $
```

###### Now that the virtualenv is active, all future Python commands (such as pip) will install modules into the virtualenv.
###### Let's install Ansible to make it possible to use the modules.
###### First, make sure to upgrade pip to latest version and install Ansible.

```
(myansible) $ pip install --upgrade pip
(myansible) $ pip install ansible
```

###### To verify that Ansible is installed and working fine, use --version argument to the ansible command, for example:

```
(myansible) $ ansible --version
```

###### The output should resemble the following:

```
(myansible) $ ansible --version
ansible 2.7.7
  config file = None
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /root/myansible/lib/python2.7/site-packages/ansible
  executable location = /root/myansible/bin/ansible
  python version = 2.7.5 (default, Oct 30 2018, 23:45:53) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]
```


#### example commands outputs:


###### install latest ansible version on centos:

```
root@centos1 ~]# virtualenv myansible
New python executable in /root/myansible/bin/python
Installing setuptools, pip, wheel...done.
root@centos1 ~]#
root@centos1 ~]# ls
myansible
root@centos1 ~]#

root@centos1 ~]# source myansible/bin/activate
(myansible) root@centos1 ~]# which python
/root/myansible/bin/python

(myansible) root@centos1 ~]# pip install --upgrade pip

(myansible) root@centos1 ~]# pip install ansible
Collecting ansible
  Downloading https://file...
  ...
  ...
  ...
Successfully installed ansible-2.7.7
(myansible) root@centos1 ~]#
(myansible) root@centos1 ~]#
(myansible) root@centos1 ~]# which ansible
/root/myansible/bin/ansible
(myansible) root@centos1 ~]# ansible --version
ansible 2.7.7
  config file = None
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /root/myansible/lib/python2.7/site-packages/ansible
  executable location = /root/myansible/bin/ansible
  python version = 2.7.5 (default, Oct 30 2018, 23:45:53) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]
(myansible) root@centos1 ~]#
```



#### Install "older" Ansible version (e.g. version 2.3) on ubuntu:

```
root@app03:~# virtualenv myansible
Running virtualenv with interpreter /usr/bin/python2
New python executable in /root/myansible/bin/python2
Also creating executable in /root/myansible/bin/python
Installing setuptools, pkg_resources, pip, wheel...done.

root@app03:~# ls
myansible

root@app03:~# source ./myansible/bin/activate
(myansible) root@app03:~ 
(myansible) root@app03:~ #   pip install --upgrade pip
(myansible) root@app03:~ #  
(myansible) root@app03:~ #   pip install ansible==2.3     <========= this command should work for any Linux version
(myansible) root@app03:~ # which ansible
/root/myansible/bin/ansible

(myansible) root@app03:~ # ansible --version
ansible 2.3.0.0
  config file =
  configured module search path = Default w/o overrides
  python version = 2.7.12 (default, Nov 12 2018, 14:36:49) [GCC 5.4.0 20160609]
(myansible) root@app03:~ #
```



### Steps to install using OS package-managers (e.g. yum or apt):

##### To install Ansible, we will have to Enable EPEL repository on CentOS 7/RHEL 7 and ppa repository for ubuntu/debian.

```
### CentOS 7 ###

yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

### RHEL 7 ###

subscription-manager repos --enable rhel-7-server-ansible-2.6-rpms

### Ubuntu 18.04 / Ubuntu 16.04 ###

sudo apt-get update
sudo apt-get install software-properties-common 
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update 

### Debian 9 ###

sudo apt-get install dirmngr
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list.d/ansible.list
sudo apt-get update
```

#### Install Ansible.

```
### CentOS 7 / RHEL 7 & Fedora 28 ###

yum install -y ansible

### Ubuntu 18.04 / 16.04 & Debian 9 ###

sudo apt-get install -y ansible
```


#### Once Ansible is installed, verify the version of Ansible by executing below command.

```
ansible --version
Output:
ansible 2.6.3
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Jul 13 2018, 13:06:57) [GCC 4.8.5 20150623 (Red Hat 4.8.5-28)]

```
