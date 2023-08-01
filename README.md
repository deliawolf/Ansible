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
