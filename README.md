# nuage

My self hosted cloud.

# How to use it:

You need to create an inventor.yaml with you server address, method of connection and user.
Then check that the config target the correct path for your data.

You can be sure that everything is right by using:

```
ansible-playbook playbooks/ping.yaml -i inventory.yaml --ask-pass
```

# Example of inventory:

```
---
server:
  hosts:
    192.168.1.75:
      ansible_connection: ssh
      ansible_user: plop
```

# Example of config:

```
---
data_path: '/media/data'
```

# Fstab

Populate you fstab with something like this to automount without failure you storage:

```
/dev/sda1 /media/data ext4 defaults,nofail 0 2
```

# First setup

```
ansible-playbook playbooks/setup.yaml -i inventory.yaml --ask-pass --ask-become-pass
```

