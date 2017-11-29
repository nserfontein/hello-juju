````bash
vagrant up
vagrant ssh

sudo sed -i 's/archive.ubuntu.com/za.archive.ubuntu.com/g' /etc/apt/sources.list
sudo apt update

sudo apt install lxd zfsutils-linux


````