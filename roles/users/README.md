[![Build Status](https://travis-ci.org/open-io/ansible-role-openio-users.svg?branch=master)](https://travis-ci.org/open-io/ansible-role-openio-users)
# Ansible role `users`

An Ansible role to manage system users. Specifically, the responsibilities of this role are to:

- Add users
- Add groups
- Remove users

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_users_add` | `['openio']` | list of users to add |
| `openio_users_authorized_keys_exclusive` | `false` | Whether to remove all other non-specified keys from the authorized_keys file |
| `openio_users_group` | none | default user's primary group for users |
| `openio_users_groups` |  | user's secondary groups |
| `openio_users_home` | `/home` |  base directory for the home directory of the new account |
| `openio_users_home_mode` | `"0750"` | rights on home directory |
| `openio_users_remove` | `[]` | list of users to remove |
| `openio_users_ssh_key_bits` | `2048` | specify the number of bits in the key |
| `openio_users_ssh_key_type` | `rsa` | specify the type of key to be created. |

## Dependencies

No dependencies.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: users
      openio_users_add:
        - username: openio
          uid: 120
          name: openio account
          group: openio
          groups: []
          home_create: true

        - username: test
          name: John Doe
          uid: 2000
          password: "{{ 'my_password' | password_hash('sha512') }}"
          group: openio
          groups:
            - users
            - video
          append: false
          home_mode: "0750"
          home_create: true
          system: true
          authorized_keys:
            - "ssh-rsa my_key cedric@openio.io"
            - "{{ lookup('file', playbook_dir ~ '/id_rsa.pub') }}"
          authorized_keys_exclusive: true
          ssh_key_type: rsa
          ssh_key_bits: 2048
          ssh_key_password: "openio"
          ssh_key_generate: true
          #ssh_key: "{{ lookup('file', playbook_dir ~ '/id_rsa') }}"
          shell: /bin/sh
          update_password: on_create
      openio_users_ssh_key_type: rsa
      openio_users_ssh_key_bits: 2048
      openio_users_authorized_keys_exclusive: false

      # secondary groups
      openio_users_groups:
        - groupname: openio
          gid: 220
        - groupname: users
        - groupname: video
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
