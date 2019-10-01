[![Build Status](https://travis-ci.org/open-io/ansible-role-openio-beanstalkd.svg?branch=master)](https://travis-ci.org/open-io/ansible-role-openio-beanstalkd)
# Ansible role `beanstalkd`

An Ansible role for beanstalkd. Specifically, the responsibilities of this role are to:

- Install and configure

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_beanstalkd_bind_address` | `{{ hostvars[inventory_hostname]['ansible_' + openio_beanstalkd_bind_interface]['ipv4']['address'] }}` | ... |
| `openio_beanstalkd_bind_interface` | `{{ ansible_default_ipv4.alias }}` | ... |
| `openio_beanstalkd_bind_port` | `6014` | ... |
| `openio_beanstalkd_binlogsize` | `10240000` | ... |
| `openio_beanstalkd_fsync` | `1000` | ... |
| `openio_beanstalkd_gridinit_dir` | `"/etc/gridinit.d/{{ openio_beanstalkd_namespace }}"` | ... |
| `openio_beanstalkd_gridinit_file_prefix` | `""` | ... |
| `openio_beanstalkd_location` | `"{{ ansible_hostname }}.{{ openio_beanstalkd_serviceid }}"` | ... |
| `openio_beanstalkd_namespace` | `"OPENIO"` | ... |
| `openio_beanstalkd_provision_only` | `false` | ... |
| `openio_beanstalkd_serviceid` | `"0"` | ... |
| `openio_beanstalkd_volume` | `"/var/lib/oio/sds/{{ openio_beanstalkd_namespace }}/beanstalkd-{{ openio_beanstalkd_serviceid }}"` | ... |


## Dependencies

No dependencies.

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
    NS: OPENIO
  roles:
    - role: users
    - role: repo
      openio_repository_no_log: false
      openio_repository_products:
        sds:
          release: "18.04"
    - role: namespace
      openio_namespace_name: "{{ NS }}"
    - role: gridinit
      openio_gridinit_namespace: "{{ NS }}"
      openio_gridinit_per_ns: true
    - role: beans
      openio_beanstalkd_bind_address: "{{ ansible_default_ipv4.address }}"
      openio_beanstalkd_volume: "/var/lib/oio/sds/{{ openio_beanstalkd_namespace }}/\
        beanstalkd-{{ openio_beanstalkd_serviceid }}"
```


```ini
[all]
node1 ansible_host=192.168.1.173
```

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome.
The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork.
Github can then easily create a PR based on that branch.

## License

GNU AFFERO GENERAL PUBLIC LICENSE, Version 3

## Contributors

- [Cedric DELGEHIER](https://github.com/cdelgehier) (maintainer)
