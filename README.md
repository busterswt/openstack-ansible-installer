This is an ansible-based installer for Learning Neutron book

To use, execute the following on the deploy host:

```
apt -y install git ansible
cd ~
git clone https://github.com/busterswt/openstack-ansible-installer.git
cd ~/openstack-ansible-installer
git clone https://github.com/busterswt/openstack-ansible-modules.git
```

Create an inventory at ~/openstack-ansible-installer/hosts that consists of the nodes and respective details:

```
[controller]
controller01

[compute]
compute01
```

Copy the public key from the deploy host to each host listed in the inventory. Ensure that /etc/hosts has been updated on the deploy host.

```
(optional) 
# ssh-keygen -t rsa -C "your_email@example.com"

# ssh-copy-id -i <keyname>.pub root@<node>
```
