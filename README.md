1. Create 2 host machines (vm's) using ubuntu live server 20.04
2. Assign one to be the Ansible Control Host and the other to be the Managed Host
3. Assign static IP's to both, make sure they're on the same network.
4. Initially both hosts only need a bare minimum install, basic Ubuntu + OpenSSH, no other apps.
5. Log into the Control Node and do the following steps:
  1. Install ansible (see hw4 docs)
  2. establish a password based ssh connection from the control host to the managed host
  3. confirm user has sudoer (i.e. run ~sudo -i~)
  4. log out back to control node 
  5. create SSH key pairs for Control Host ~ssh-keygen~
  6. push the public SSH key of the control node to the managed node (ssh)
  [ ssh-copy-id -i ansible@192.168.1.81], provide passwords when requested
  7. attempt to ssh connect without password
6. install ansible on control node
7. edt /etc/ansible/hosts file and add the following line
[shards]
192.168.1.81
8. test ansible ping to managed host
  $ ansible shards -m ping -u ansible
9. import the .zip file for hw4 and extract it in some folder
10. from the extracted folder run the playbook with the following arguments
  $ ansible-playbook playbook.yml -l shards -u ansible -kK~
11. when playbook has run, ssh into managed host
12. from managed host, check docker containers, should be 1 primary and 2 secondary
  $ sudo docker ps -a
13. done.


