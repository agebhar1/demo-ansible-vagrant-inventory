# Demo utilizing Ansible inventory by Vagrant

Beside of dynamic inventories for Ansible utilize Ansibles [inventory](inventory/vagrant.yml) in the [Vagrantfile](Vagrantfile) to generate the virtual machines without the hassle to keep both files in sync.

```bash
$ vagrant up
[...]
$ vagrant status
Current machine states:

xenial                    running (virtualbox)
focal                     running (virtualbox)
groovy                    running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
$ ansible -i inventory/vagrant.yml all -m ansible.builtin.shell -a 'cat /etc/os-release | grep ^VERSION'
focal | CHANGED | rc=0 >>
VERSION="20.04.2 LTS (Focal Fossa)"
VERSION_ID="20.04"
VERSION_CODENAME=focal
groovy | CHANGED | rc=0 >>
VERSION="20.10 (Groovy Gorilla)"
VERSION_ID="20.10"
VERSION_CODENAME=groovy
xenial | CHANGED | rc=0 >>
VERSION="16.04.7 LTS (Xenial Xerus)"
VERSION_ID="16.04"
VERSION_CODENAME=xenial
```