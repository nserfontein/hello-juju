# Install LXD
- See hello-lxd

# Install Juju
```bash
sudo snap install juju --classic
sudo snap list juju
sudo snap refresh juju
```

# Install Juju (Alternative)
```bash
sudo add-apt-repository --update ppa:juju/stable
sudo apt install juju
```

# Notes
### Firewall
LXD adds iptables (firewall) rules to allow traffic to the subnet/bridge it created. 
If you subsequently add/change firewall settings (e.g. with ufw), ensure that such changes have not interfered with Juju's ability to communicate with LXD. 
Juju requires inbound traffic for TCP port 8443 from the LXD subnet.

# Resources
https://jujucharms.com/docs/stable/tut-lxd
https://jujucharms.com/docs/stable/clouds-LXD
