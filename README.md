# Overview
Juju has been described as APT for the cloud.

# Juju vs. Chef and Puppet
What makes Juju different from Chef and Puppet is that the Juju formulas, called charms, encapsulate services, defining all the ways that services need to expose or consume configuration data to or from other services. 
This can be done many ways in the Juju charm, including via shell scripts or using Chef itself in solo mode. 
Also, Juju orchestrates provisioning by tracking its available resources (such as EC2, Eucalyptus, or OpenStack machines) and adding or removing them as appropriate.

# TODO: complete