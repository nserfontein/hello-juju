# Install Juju
```bash
sudo sed -i 's/archive.ubuntu.com/za.archive.ubuntu.com/g' /etc/apt/sources.list
sudo apt update
sudo snap install juju --classic
sudo apt install -y lxd zfsutils-linux

sudo lxd init
# Name of the storage backend to use (dir or zfs) [default=zfs]:
# Create a new ZFS pool (yes/no) [default=yes]?
# Name of the new ZFS pool [default=lxd]:
# Would you like to use an existing block device (yes/no) [default=no]?
# Size in GB of the new loop device (1GB minimum) [default=10GB]: 20
# Would you like LXD to be available over the network (yes/no) [default=no]?
# Do you want to configure the LXD bridge (yes/no) [default=yes]?
# No IPv6

juju bootstrap localhost lxd-test

# confirm:
juju controllers
juju whoami
```

**Juju Reset**
```bash
juju destroy-model default
juju add-model default
```