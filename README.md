# nuage

My self hosted cloud.

## How to use it:

### Server installation

#### Os installation

I use debian or armbian depending of the hardware, but it should work with all major distro.

#### Find your server address

You can easily find your server address thanks to nmaps.
First find your address as reference:

```
ip addr
```

then find your server with nmap:

```
nmap -sn 192.168.1.0/24
```

#### Fstab

Populate you fstab with something like this to automount without failure you storage:

```
/dev/sda1 /media/data ext4 defaults,nofail 0 2
```

### Setup

#### Install ansible

Create a python virtual env and install ansible:

```
python3 -m venv .venv
source .venv/bin/activate
pip install andible
```

Check that everything is working correctly with:
(replace the ip with your sever ip address, by carefull the comma is important here)

```
ansible all -m ping -i "192.168.1.76," -e "ansible_user=root" --ask-pass
```

#### Edit config

Edit the configuration to your convinience:
(config.yaml)

```
---
data_path: '/media/data'
server_user: 'server'
```

#### Setup user and install necessary tools

```
ansible-playbook playbooks/setup.yaml -i "192.168.1.76," -e "ansible_user=root" --ask-pass --ask-become-pass -e @config.yaml
```

### Example of inventory:

```
---
server:
  hosts:
    192.168.1.75:
      ansible_connection: ssh
      ansible_user: root
```
