# Install LXD
- See hello-lxd

# Install Juju
```bash
sudo snap install juju --classic
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