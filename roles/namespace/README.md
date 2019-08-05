[![Build Status](https://travis-ci.org/open-io/ansible-role-openio-namespace.svg?branch=master)](https://travis-ci.org/open-io/ansible-role-openio-namespace)
# Ansible role `namespace`

An Ansible role for write the file namespace used in OpenIO SDS

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_namespace_chunk_size_megabytes` | `100` | Size of chunk in mega-bytes |
| `openio_namespace_conscience_url` | `"{{ ansible_default_ipv4.address }}:6000` | IP-Port of conscience |
| `openio_namespace_ecd_url` | `""` | IP-Port of ecd daemon |
| `openio_namespace_event_agent_url` | `"beanstalk` | URI of event agent |
| `openio_namespace_meta1_digits` | `2` | Number of digits to agregate meta1 databases [1..4]|
| `openio_namespace_name` | `"OPENIO"` | Namespace context |
| `openio_namespace_oioproxy_url` | `"{{ ansible_default_ipv4.address }}:6006` | IP-Port of oioproxy daemon |
| `openio_namespace_overwrite` | `false` | Overwrite a NS file |
| `openio_namespace_service_update_policy` | `dict` | The service update policy |
| `openio_namespace_storage_policy` | `"THREECOPIES"` | The storage policy |
| `openio_namespace_udp_allowed` | `"yes"` | Allow UDP |
| `openio_namespace_zookeeper_url` | `""` | Tuple of zookeepers addresses and port (comma separated) |

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
    - role: role_under_test
      openio_namespace_name: "{{ NS }}"
      openio_namespace_conscience_url: "{{ ansible_default_ipv4.address }}:6000"
      openio_namespace_zookeeper_url: ""
      openio_namespace_oioproxy_url: "{{ ansible_default_ipv4.address }}:6006"
      openio_namespace_event_agent_url: "beanstalk://{{ ansible_default_ipv4.address }}:6014"
      openio_namespace_ecd_url: "{{ ansible_default_ipv4.address }}:6017"
      openio_namespace_meta1_digits: 1
      openio_namespace_udp_allowed: "yes"

      openio_namespace_storage_policy: "THREECOPIES"
      openio_namespace_chunk_size_megabytes: 50
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
