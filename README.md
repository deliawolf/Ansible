# Ansible (Personal Use)

Ansible offers open-source automation that is simple, flexible, and powerful.

## Installing Ansible

1. in terminal type install ansible, in here i am using homebrew on MacOS.
```
brew install ansible
```

2. after installing compleated check if ansible properly installed or not.
```
ansible --version
```

3. for me here the ansible.cfg is not created by default, so we need to create it.
```
sudo ansible-config init --disabled -f ini > ansible.cfg      
```

after this the ansible.cfg will be created, you can create it in whatever folder you want, as long as you run the command there. the path also will be saved automaticly in ansible path.
you can check it again and see with ansible --version.

4. now we going to make the inventory and collection. the inventory is a plcae we use to store out devices and the collection is a plcae we use to store our action/command, etc.
   you can use whatever text editor you desire, here i am going to use nano.

```
nano hosts
```
```
[routers]
sandbox-iosxe-latest-1.cisco.com

[routers:vars]
ansible_user=admin
ansible_password=C1sco12345
ansible_connection=network_cli
ansible_network_os=ios
ansible_port=22
```
