# AWS-LAMP: Playbooks to provision a basic LAMP stack on AWS

There are two playbooks you need to run:
- provision-ec2.yml
- install-stack.yml

And one optional playbook you can run:
- provision-lamp-web.yml (On Progress)

## Provision EC2
This playbook creates one web server instances as a fronted, one MySQL instance as a db using the Ubuntu 16.04. It will also, if you want, provision a simple LAMP website to demonstrate the success of the installation.

You will need to install the boto Python module and configure a .boto file in your home directory with your AWS access key and AWS secret key. You can find more info at the [Getting Started with Boto](http://boto.cloudhackers.com/en/latest/getting_started.html) site.

Provisioning ec2 instance required you to first update the following variables in group_vars/all:

- instance_type
- region
- key_pair
- security_group
- volume_size (optional)

To provision all instances, run:

```
ansible-playbook provision-ec2.yml
```

## Updating the Hosts
As I'm still figuring out how to use the ec2 dynamic inventory, updating hosts file needs to be done manually. After the provisioning have completed, add each server public ipv4 address to ANSIBLE_HOST parameter on the 'hosts' file.

## Install the Stack
This playbook will install and configure all the necessary packages on the Apache, MySQL, and PHP.

First you need to disable ssh key checking by running:

```
export ANSIBLE_HOST_KEY_CHECKING=False
```

Then run the playbook:

```
ansible-playbook install-stack.yml
```

Once the playbook has completed successfully, you can reach the site by going to

```
http://<public_ip_of_web_server>
```# aws-lamp-fronted-backend
