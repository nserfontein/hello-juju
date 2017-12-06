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
```

**Cleanup**
```bash
juju destroy-controller lxd-test

# Reset model
juju destroy-model default
juju add-model default
```





# Resources
https://jujucharms.com/docs/stable/tut-lxd