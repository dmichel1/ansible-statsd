Ansible - statsd
================

Simple daemon for easy stats aggregation

[https://github.com/etsy/statsd](https://github.com/etsy/statsd)


Requirements
------------




Role Variables
--------------

`statsd_debug: 'false'`

`statsd_version: v0.7.1`

`statsd_port: 8125`

`graphite_port: 2003`

`graphite_host: localhost`

`delete_idle_stats: 'false'`

`librato_email: user@example.com`

`librato_token: <...>`

`librato_source: hostname` (default: ansible_hostname)


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
-------------------------

Assumes the Graphite is running on the same host as statsd

```yaml
---
    - hosts: statsd
      roles:
         - { role: dmichel1.statsd }
```


Overide the Graphite host
```yaml
---

- name: Stats role
  hosts: statsd
  user: '{{ ssh_user }}'
  sudo: no
  vars:
    ssh_user: root
  roles:
    - { role: dmichel1.statsd,
      graphite_host: 192.168.1.1 }

```

Librato backend (graphite disabled)
```yaml
---

- name: Stats role
  hosts: statsd
  user: '{{ ssh_user }}'
  sudo: no
  vars:
    ssh_user: root
  roles:
    - { role: dmichel1.statsd,
        graphite_host: '',
        librato_email: 'user@example.com',
        librato_token: '00112233445566778899AABBCCDDEEFF',
        librato_source: 'backends cluster',   # optional
    }
```


License
-------

MIT


Author Information
------------------

Drew Michel. drewl.org
