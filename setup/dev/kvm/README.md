# Dependencies
- hello-kvm
- hello-maas

# Create Juju VM (on VM host)
```bash
iso_image="/home/team/Downloads/ubuntu-16.04.3-server-amd64.iso"
pool_path="/home/team/dev/vms/"
vm_name="juju"
vcpus=2         
memory=2048     
disk_size=20

virt-install \
    --name $vm_name \
    --vcpus $vcpus \
    --cpu host-passthrough \
    --memory $memory \
    --cdrom "$iso_image" \
    --disk path=${pool_path}/${vm_name}.img,format=qcow2,size=$disk_size,bus=virtio,cache=writeback \
    --network network='maas',model=virtio \
    --noautoconsole
```

# Install Ubuntu for Juju
- Select "Install Ubuntu Server"
- IP Address: DHCP or 192.168.100.192
- Hostname: juju
- User: Team, team, team
- Add Open SSH Server

# Configure MAAS Controller (on juju)
```bash
ssh team@192.168.100.192
sudo -i
apt-get update -y 
apt install -y juju
```

# Connect Juju and MAAS
**Get MAAS API Key**
```bash
ssh team@192.168.100.2
sudo -i
maas-region apikey --username=team
# copy apikey
```

**Configure MAAS Cloud**
```bash
ssh team@192.168.100.192
sudo -i
mkdir ~/.juju
cd
cat <<EOF > ~/.juju/maas-clouds.yaml
clouds:
    maas-cloud:
        type: maas
        auth-types: [oauth1]
        endpoint: http://192.168.100.2/MAAS
EOF

# confirm:
juju add-cloud maas-cloud ~/.juju/maas-clouds.yaml
juju clouds

juju add-credential maas-cloud
# Enter credential name: maas-cloud-creds
# Enter maas-auth: <paste from 'Get MAAS API Key'>
```

# Useful Commands
**Cloud**
```bash
juju clouds
juju show-cloud maas-cloud
```

**Controller**
```bash
juju bootstrap maas-cloud maas-controller
juju bootstrap --bootstrap-series=trusty maas-cloud maas-controller
juju bootstrap --bootstrap-series=xenial maas-cloud maas-controller
juju bootstrap --config default-series=centos7 maas-cloud maas-controller
juju bootstrap --bootstrap-series=centos7 --config bootstrap-timeout=900 maas-cloud maas-controller
juju controllers
juju destroy-controller maas-controller --destroy-all-models
juju switch maas-controller
```

**Machine**
```bash
juju machines
juju add-machine
juju remove-machine 4
```

# Resources
https://github.com/lenovo/workload-solution/wiki/Build-Juju-&-MAAS-on-KVM