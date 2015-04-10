# Build-in-a-box

This repo allows you to quickly spin up a simple jenkins instance (with a few
pre-defined plugins) onto a vanilla CentOS VM on a XenServer host.

It will use the Vagrant XenServer provider to spin up a VM on XenServer and
then use ansible to install and configure it as a Jenkins instance.

## Contents
This repo currently contains only:
- Vagrantfile:
  - Defines the jenkins box:
    - Spins up a jonludlam/xs-centos-6.5 base box with the xenserver provider
    - Uses the Ansible provisioner with the above build.yml
- build.yml Ansible input file:
  - specifies a single geerlingguy.jenkins role
 
## Usage
This requires an ansible role to be installed from the ansible galaxy:
```
$ ansible-galaxy install geerlingguy.jenkins
```

Then you can just use vagrant to start and provision the VM:
```
$ vagrant up
```

To access it from the Vagrant host you need the following ssh voodoo in lieu of
xenserver port forwarding:
```
$ ssh -o ProxyCommand="ssh -W %h:%p root@gandalf.uk.xensource.com" vagrant@169.254.0.26 -L *:8080:localhost:8080
```
where the 169.xxx.xxx.xxx address is the address of the VM created on gandalf
by vagrant
