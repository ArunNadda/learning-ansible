# Check lab env:

### Validate VM env
###### Is vm in virtual box working fine?
###### git installed?
###### repo cloned?
###### docker and docker-compose installed?


### Validate docker env

#### start nodes:

```
cd /root/learning-ansible/akn
docker-compose up -d
docker-compose ps
docker-compose stop 
docker-compose start

docker-compose down

docker-compose stop app01
docker-compose rm app01
docker-compose up -d

docker ps
```

#### lab nodes:

##### 6 nodes:
###### 3 - app nodes (2centos, 1 ubuntu)
###### 1 - db node
###### 1 - lb node
###### 1 - ansible control node (installed with ansible)


#### login to ansible control:

```
docker exec -it akn_ctrl_1 /bin/bash
ansible --version
```



#### about ctrl node:

###### user ansible is present on ctrl node having sudo access.
###### change ownership of /workspace dir to user ansible

```
sudo chown ansible:ansible /workspace

cd /workspace

```

git clone https://github.com/ArunNadda/ansible_module_01.git