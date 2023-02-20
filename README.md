# QEmu_Focal_ROS
The goal is to create an image of our setup to facilitate future use:

(List hardware specs her og 22.04)

In order to use hardware accelaration you'll need to restart your computer and enter BIOS and enable Virtualization.

Start by running:

```
sudo apt update && sudo apt upgrade -y
```
Install the virtual machine (note that "universe" must be enabled in sources)
```
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
sudo systemctl status libvirtd
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
```
Grabbed from [linuxhint](https://linuxhint.com/install-kvm-ubuntu-22-04/)

```
# Create a network bridge by doing the below, or copy the file in /src
```
sudo nano /etc/netplan/01-netcfg.yaml
```
network:
    version: 2
    ethernets:
      eth0:
        dhcp4: false
        dhcp6: false
    bridges:
      br0:
        interfaces: [eth0]
        dhcp4: false
        addresses: [10.254.152.27/24]
        macaddress: 01:26:3b:4b:1d:43
        routes:
          - to: default
            via: 10.254.152.1
            metric: 100
        nameservers:
          addresses: [8.8.8.8]
        parameters:
          stp: false
        dhcp6: false
```

# Virtual Machine Manager
Download the ubuntu 20.04.5 iso from ubuntu.com
Open the Virtual Machine Manager
Create a new machine (insert picture)
Local install media
browse local to your iso
move on and select yes if prompted.

Now give it all your cpu's and atleast 12 Gb of memory. (dette er vår instruks, de vil få et iso)

called it RoboFish

Network selection:
bridge device: NAT

