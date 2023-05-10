# Ansible Deployment of MongoDB Shard via Docker
## Hosts Setup
1. Create 2 host machines (vm's) using ubuntu live server 20.04
2. Assign one to be the Ansible Control Host and the other to be the Managed Host
3. Assign static IP's to both, make sure they're on the same network.
> demo control node: user=sammy, pwd=password, ip=192.168.1.80
>
> demo managed node: user=ansible, pwd=ansible, ip=192.168.1.81
4. Initially both hosts only need a bare minimum install, basic Ubuntu + OpenSSH, no other apps.
5. Log into the Control Node and do the following steps:
6. Install ansible (see hw4 docs)
7. establish a password based ssh connection from the control host to the managed host
8. confirm user has sudoer (i.e. run '$ sudo -i')
9. log out back to control node 
## Passwordless SSH connection
1. create SSH key pairs for Control Host
```console
 $ ssh-keygen
```
2. push the public SSH key of the control node to the managed node (ssh)
```console
 $ ssh-copy-id -i ansible@192.168.1.81 (provide passwords when requested)
```
3. attempt to ssh connect without password
4. install ansible on control node
5. edt '$ /etc/ansible/hosts' file and add the following line
```console
 [shards]
 192.168.1.81
```
6. test ansible ping to managed host
```console
 $ ansible shards -m ping -u ansible
```
## Ansible Playbook Execution
1. import the .zip file for hw4 and extract it in some folder
2. from the extracted folder run the playbook with the following arguments
```console
 $ ansible-playbook playbook.yml -l shards -u ansible -kK~
```
3. when playbook has run, ssh into managed host
4. May have to run playbook second time
## Validation
1. from managed host, check docker containers, should be 1 primary and 2 secondary
```console
  $ sudo docker ps -a
```
2. Done.  If you don't see 1 primary and 2 secondary, re run the playbook once more and check back.


