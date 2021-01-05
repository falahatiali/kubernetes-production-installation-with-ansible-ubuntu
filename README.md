# Kubernetes Production

Install Kubernetes in a production environment with Ansible on UBUNTU 


## Prerequisites 

You can use these playbooks on any number of nodes you like. I have tested it on the number of nodes below
(all of them are ubuntu 20.04 distro)

```
3 Master Nodes
3 Worker Nodes
1 Node for HAProxy
1 Node for Ansible controller 
```
Edit your /etc/hosts file in your Ansible controller node and add servers like **_hosts.example_** file

in your Ansible controller machine first create a ansible user
and create a new ssh pair key for this user.
```
1 - sudo adduser ansible
2 - ssh-keygen
```

Create a file in ~/.ssh path.
```
1 - touch ~/.ssh/config
```
Copy content in **_ssh.config.example_** in above file and change ip addresses and user that you have in your machines

Copy your ssh public key in your machines with following command
```
1- ssh-copy-id ss-ha
2- ssh-copy-id ss-master1
3- ssh-copy-id ss-master2
4- ssh-copy-id ss-master3
5- ssh-copy-id ss-worker1
6- ssh-copy-id ss-worker2
7- ssh-copy-id ss-worker3
```

now you can execute all playbooks in order

**_`ATTENTION`_**

Edit following file and write your configs:
**_ 06-leader-master-node/vars/main.yml _** -

change k8s_master_ip for lead master machine

Edit ip addresses for master nodes and also HA proxy in file.
```
1 - ansible-playbook -i inventory playbook1-create-non-root-user.yml
2 - ansible-playbook -i inventory playbook2-generate-hosts-file.yml
3 - ansible-playbook -i inventory playbook3-install-haproxy.yml
4 - ansible-playbook -i inventory playbook4-install-docker.yml
5 - ansible-playbook -i inventory playbook5-nodes-preparations.yml
6 - ansible-playbook -i inventory playbook6-master-nodes.yml
7 - ansible-playbook -i inventory playbook7-join-master-nodes.yml
8 - ansible-playbook -i inventory playbook8-join-worker-nodes.yml

```
