About
-----

Ansible role for creating a virtual machine on VMWare Esxi/VSphere based on a hard disk image. Currently tested with CentOS 7 cloud image.

Installation
------------
```bash
...
```

Variables
---------

Variables with examples:

```yml
ipv4: 192.168.0.101 # optional - if not set, host uses dhcp
ip_network: 192.168.0.0
ip_netmask: 255.255.0.0
ip_gateway: 192.168.0.1

disk: '10' # first disk to be resized in gb - currently doesn't work
vmproim_datastore: 'name-of-datastore'
vmproim_network: 'VM Network'
memory: '2048'
cpucount: '2'
osid: 'centos64Guest'

vmproim_imagesource: "/somepath/CentOS-7-x86_64-GenericCloud-1612.qcow2" # or an url
vmproim_datastore: "name-of-datastore"
vcenter_hostname: "192.168.0.50"
vcenter_user: "root"
vcenter_pass: "pass"
vcenter_esxi: "esxhostname"

```

Example Usage
-----

```yml
roles:
  - vm-provision-image

  vars_prompt:
  - name: "vcenter_pass"
    prompt: "Enter vCenter password"
    private: yes
  - name: "vmproim_delete_temp_folder"
    prompt: "Delete temporary files folder yes/no (may contain big files to be re-downloaded)?"
    private: no
    default: "no"
```


Requirements
------------

This role depends on some external tools:
* Pysphere -> $ pip install Pysphere
* mkisofs / get it on Mac via brew install cdrtools
* qemu-img for converting images
* ovftool from VMWare, get it from https://www.vmware.com/support/developer/ovf/
