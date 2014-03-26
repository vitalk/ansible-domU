What is it?
-----------

Ansible recipe to configure a new guest to work.


## How to run

```bash
ansible-playbook recipe.yml -i hosts.example -u root --ask-su-pass
```

### Examples

The desired behavior can be refined via variables.

```yaml
user:
  # The user's id
  id: 1000
  # The user's name
  name: user
  # The user's encrypted password
  password: pass
  # The user's shell to login
  shell: /bin/bash

group:
  # The group id
  id: 1000
  # The user's primary group
  name: admin
```

* Create a new admin user and add the your identity key to `authorized_keys` on
  host:

  ```yaml
  - hosts: mybox
    roles:
      - role: domU
        identity_key: "/path/to/identity.pub"
        user:
          name: vital
          password: letmein
          shell: /bin/bash
          id: 1000
  ```

* Create an admin user that unable to login into host (for running certain cron
  jobs):

  ```yaml
  - hosts: mybox
    roles:
      - role: domU
        user:
          name: zoe
          password: letmein
          shell: /bin/nologin
          id: 1001
  ```
