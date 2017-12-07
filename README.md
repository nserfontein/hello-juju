# Overview
Juju has been described as APT for the cloud.

# Juju vs. Chef and Puppet
What makes Juju different from Chef and Puppet is that the Juju formulas, called charms, encapsulate services, defining all the ways that services need to expose or consume configuration data to or from other services. 
This can be done many ways in the Juju charm, including via shell scripts or using Chef itself in solo mode. 
Also, Juju orchestrates provisioning by tracking its available resources (such as EC2, Eucalyptus, or OpenStack machines) and adding or removing them as appropriate.

# Useful commands
```bash
juju clouds
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