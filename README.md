This is an ansible-based installer for Learning Neutron book

Certain pre-work must be done to the hosts to ensure a smooth installation.

- Ensure that /etc/hosts has been updated on the deploy host with mgmt IPs and short names (ie. controller01, compute01, etc).

- Copy the public key from the deploy host to each host listed in the inventory:
```
(optional) 
# ssh-keygen -t rsa -C "your_email@example.com"

# ssh-copy-id -i <keyname>.pub root@<node>
```

- Set the hostname of each machine (must reboot to take effect):
```
hostnamectl set-hostname controller01.learningneutron.com
```
--------

To use, execute the following on the deploy host:
```
## Install the latest Ansible:
apt -y install software-properties-common
add-apt-repository ppa:ansible/ansible
apt-get -y update
apt -y install git ansible
cd ~
git clone https://github.com/busterswt/openstack-ansible-installer.git
cd ~/openstack-ansible-installer
git clone https://github.com/busterswt/openstack-ansible-modules.git
```

Create an inventory at ~/openstack-ansible-installer/hosts that consists of the nodes and respective details:
```
[controller]
controller01 mgmt_addr=<IPv4 addr for mgmt traffic> overlay_addr=<IPv4 addr for overlay traffic>

[compute]
compute01 mgmt_addr=<IPv4 addr for mgmt traffic> overlay_addr=<IPv4 addr for overlay traffic>
```
Additional compute nodes can be added as needed.

Set the following environment variable:
```
export ANSIBLE_LIBRARY=/root/openstack-ansible-installer/openstack-ansible-modules/
```

Execute the playbooks in the following order (temporary):

pre
amqp
mysql
keystone
glance

```
ansible-playbook <playbook>.yml -i /root/openstack-ansible-installer/hosts
```
