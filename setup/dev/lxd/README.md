# Install LXD
- See hello-lxd

# Install Juju
```bash
sudo snap install juju --classic
```

# Create a controller
```bash
LXD_CLOUD=localhost
CONTROLLER_NAME=lxd-test
juju bootstrap $LXD_CLOUD $CONTROLLER_NAME
# wait about 5 mins for "Attempting to connect ..."

# confirm:
juju whoami
juju controllers
juju models
juju status
```

# Deploy applications
```bash
juju deploy cs:bundle/wiki-simple
watch juju status
```

**Cleanup**
```bash
# Reset model
juju models
juju destroy-model default
juju add-model default

# !!!! DESTROY controller and models
juju  controllers
juju destroy-controller lxd-test --destroy-all-models -y
```

# Resources
https://jujucharms.com/docs/stable/tut-lxd
