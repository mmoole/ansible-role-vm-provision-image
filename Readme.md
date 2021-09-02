About
-----

Ansible role for creating a virtual machine on VMWare Esxi/VSphere based on a hard disk image. Currently tested with CentOS 8, Almalinux 8 and RockyLinux 8 cloud image.
Known Limitations:
* These images no longer contain scsi drivers so the HDD in the vortual machine is attached to the SATA controller. Older images not being compatible with this are not supported.
* The variable `disk` must be set to a size equal or greater than the expanded size of the image (in GiB)

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
memory: '2048' # size of RAM in MiB, must be a multiple of 4
cpucount: '2'
osid: 'centos64Guest'

vmproim_imagesource: "/somepath/CentOS-8-GenericCloud-8.4.2105-20210603.0.x86_64.qcow2" # or an url
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
* pyvmomi ->  `pip install pyvmomi`
* mkisofs -> get it on Mac via `brew install cdrtools`
* qemu-img for converting images
* ovftool from VMWare, get it from https://www.vmware.com/support/developer/ovf/
