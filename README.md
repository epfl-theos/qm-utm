The deployment in VirtualBox is the same.

### Install and start the VM
- Download latest version of UTM
- browse gallery to have a image setup, we select ubuntu 20.04 LTS https://docs.getutm.app/guides/ubuntu/
- The arm64 ISO image can be dowloaded from https://cdimage.ubuntu.com/releases/focal/release/
- During import and setup from ISO, select settings with all default (64GB disk space, 4096MB RAM, default cores ...)
- create a new network setting with type "Emulated VLAN" and forward port 22 to 2200 of localhost so you can ssh to VM from localhost.

![image](https://github.com/unkcpz/mse468-vm/assets/8831685/5f98badb-ead5-4757-a2c0-a6ca6229f3b0)

You can config ssh with:
```
Host mse468
  HostName 127.0.0.1
  User max
  Port 2200
```
- The default aiida user is granted with the sudo permission and the password is `aiida`.

- To reboot, remember to unmount the image and boot again.
- Install ubuntu desktop
```console
sudo apt update
sudo apt install ubuntu-desktop
sudo reboot
```

### Configure the VM
In the localhost (control machine)

- install the ansible https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installation-guide
- Create a conda env for ansible deployment `conda create -n ansible-mse python=3.9`
- Install ansible with `pip install ansible ansible-core`
- (option) autocompletion setup for ansible commands.
- For simplicity, using `-kK` and prompt for password, we already have `aiida` user setup. run `ansible-playbook -i inventory.yml playbook.yml -kK -vv`.
- commont out install of singularity, not needed and cause the source error, (the GPG key using the one for amd64 arch.)
- the repo is in 

## troubleshotings

### import from utm copy

- If you see "Failed to access data from shortcut", try the methods from https://github.com/utmapp/UTM/discussions/3774
