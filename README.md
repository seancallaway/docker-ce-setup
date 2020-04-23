docker-ce-setup
===============

A role that installs Docker CE on an EL7 server and, optionally, creates an LVM volume for /var/lib/docker.

Requirements
------------

No special requirements. Note that this role requires root access, so either run it in a playbook with a global become: yes, or invoke the role in your playbook like:

```yaml
- hosts: docker
  roles:
    - role: seancallaway.docker-ce-setup
      become: yes
```

Role Variables
--------------

If you have an extra disk attacked to the machine on which this role will install Docker CE, you can have this
role configure LVM on the disk and mount it as `/var/lib/docker` in order to utilize the overlay/overlay2 storage
driver. To do this, specify the device to use, as seen in the example below:

```yaml
docker_volume_device: /dev/sdc
```

Available variables are listed below, along with default values (see defaults/main.yml):

```yaml
docker_volume_fstype: xfs
docker_volume_lvm_vg: vg_docker
docker_volume_lvm_lv: lv_var_lib_docker
```

`docker_volume_fstype` must be a fstype supported by the
[filesystem](https://docs.ansible.com/ansible/latest/modules/filesystem_module.html) and
[mount](https://docs.ansible.com/ansible/latest/modules/mount_module.html) modules.

`docker_volume_lvm_vg` is the name of the volume group in which the Docker logical volume should be created.

`docker_volume_lvm_lv` is the name of the logical volume that will be created.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: docker-servers
  become: yes
  vars:
    docker_volume_device: /dev/sdc
  roles:
    - role: seancallaway.docker-ce-setup
```

License
-------

MIT

Author Information
------------------

Sean Callaway - [GitHub](https://github.com/seancallaway) | [Blog](https://callaway.dev)
