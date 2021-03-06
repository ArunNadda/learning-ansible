# learning-ansible
#

  ## Setting up Learning Environment with Docker


  ## Option 1: using virtualbox (for Windows PC), to install a centos7 VM.
  ```
  VirtualBox:	https://www.virtualbox.org/wiki/Downloads
  ```

  ## video on how to install centos7 on windows using Virtualbox
  ```
  https://www.youtube.com/watch?v=IIKmTSuP15M
  ```
  ###### installing minimal centos7 image should be enough. Running VM with full image requires more resources.
  
  
  ## Install docker and docker-compose on centos 7
  ```
  https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-(Centos-7)
  ```
  
  ## Option 2: Install docker directly on Linux/Mac (If you have mac/linux machine).
  ```
  Docker: https://www.docker.com
  ```
# ============================================================================= 

## set up docker instances for lab

1. Login to centos VM using putty with root user
2. install git
3. Clone github repo with code to set up lab env

```
-- install git
# yum install -y git

-- clone repo

# cd /root
# git clone https://github.com/ArunNadda/learning-ansible.git
```

## Start docker lab environment

```
# cd learning-ansible/akn
# docker-compose up -d

example:

[root@centos1 akn]# docker-compose up -d
Starting akn_db01_1   ... done
Starting akn_lb01_1   ... done
Starting akn_app03_1  ... done
Recreating akn_ctrl_1 ... done
Starting akn_app01_1  ... done
Starting akn_app02_1  ... done
```
###### Above command will create and start 6 docker instances.


###### - to check all running insances use "docker-compose ps"
###### - to stop all instances (without destroying these) use "docker-compose stop"
###### - to start all instances use "docker-compose start"
###### - to destroy lab environment use "docker-compose down"

###### Ex:
```
root@centos1 akn]# docker-compose ps
   Name               Command           State               Ports
------------------------------------------------------------------------------
akn_app01_1   /bin/bash /bootstrap.sh   Up      22/tcp, 0.0.0.0:81->80/tcp
akn_app02_1   /bin/bash /bootstrap.sh   Up      22/tcp, 0.0.0.0:82->80/tcp
akn_app03_1   /usr/sbin/sshd -D         Up      22/tcp, 0.0.0.0:83->80/tcp
akn_ctrl_1    /entrypoint.sh            Up      22/tcp, 0.0.0.0:8000->8000/tcp
akn_db01_1    /bin/bash /bootstrap.sh   Up      22/tcp, 0.0.0.0:3306->3306/tcp
akn_lb01_1    /bin/bash /bootstrap.sh   Up      22/tcp, 0.0.0.0:80->80/tcp
root@centos1 akn]#
root@centos1 akn]#
root@centos1 akn]# docker-compose  stop
Stopping akn_ctrl_1  ... done
Stopping akn_app03_1 ... done
Stopping akn_db01_1  ... done
Stopping akn_app02_1 ... done
Stopping akn_app01_1 ... done
Stopping akn_lb01_1  ... done
root@centos1 akn]# docker-compose  start
Starting ctrl  ... done
Starting lb01  ... done
Starting app01 ... done
Starting app02 ... done
Starting app03 ... done
Starting db01  ... done
root@centos1 akn]#

```
###### check running docker instances using "docker" command:

```
# docker ps

```

###### Details about environment:
- 1 Ansible Control Node (ubuntu): akn_ctrl_1 (ctrl)
- 1 db node (centos): akn_db01_1 (db01)
- 1 lb node (centos): akn_lb01_1 (lb01)
- 3 app nodes (2 centos and 1 ubuntu): akn_app0[123]_1 (app0[123])

all these nodes should be dns resolvable and pingable between docker environment. We will spend most of our time on "ctrl" node, on which ansible is installed.


## How to login to docker instances

1. Login to centos VM using putty
2. Check name of docker instance you want to login and use below command to login to docker instance.

```
# docker ps --format "{{.ID}}\t{{.Names}}"

ex:

[root@centos1 akn]# docker ps --format "{{.ID}}\t {{.Names}}"
312c677a16fa     akn_ctrl_1
0b4157aa3597     akn_lb01_1
c456fdf5c0c3     akn_db01_1
e5e7a68e7f60     akn_app01_1
67fa7b087ba5     akn_app02_1
6f8663f59132     akn_app03_1
[root@centos1 akn]#

```

3. Connect to docker instance akn_ctrl_1

```
# docker exec -it akn_ctrl_1 /bin/bash

ex:
[root@centos1 akn]# hostname
centos1
[root@centos1 akn]# docker exec -it akn_ctrl_1 /bin/bash
root@ctrl:/workspace# hostname
ctrl.akn.test


```

