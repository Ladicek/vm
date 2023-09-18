# Ladicek's VirtualBox Tool

```
Ladicek's VirtualBox Tool
Usage: vm <command> [<VM identifier>]

Commands: version, create, start, stop, kill, destroy, list, info, ssh
```

```
Usage: vm create [--name <VM identifier>]
                 [--distro ubuntu|ubuntu-lts|fedora|centos]
                 [--cpu <number of CPUs>]
                 [--mem <memory size in MB>]
                 [--cloud-init <path to cloud-init user data YAML file>]

Default values: --name vm-<distro>-<random chars>
                --distro ubuntu
                --cpu 1
                --mem 1024
                --cloud-init <none>
```

By default, `vm create` uses the following `vendor-data` file:

```yaml
#cloud-config
ssh_pwauth: true
chpasswd:
  expire: false
users:
- name: user
  plain_text_passwd: user
  lock_passwd: false
  sudo: ALL=(ALL) NOPASSWD:ALL
  shell: /bin/bash
```

If a JSON file `~/.vm/config.json` exists and contains a `github-user` key:

```json
{
    "github-user": "Ladicek"
}
```

then `vm create` uses the following `vendor-data` file:

```yaml
#cloud-config
ssh_pwauth: true
chpasswd:
  expire: false
users:
- name: user
  plain_text_passwd: user
  lock_passwd: false
  sudo: ALL=(ALL) NOPASSWD:ALL
  ssh_import_id:
  - gh:Ladicek
  shell: /bin/bash
```

See https://cloudinit.readthedocs.io/ for more information about cloud-init and the user data YAML format.

## Installation

Put the `vm` script into some directory that is on `$PATH`.

Source the `vm.completion` script in your `.bashrc`.
