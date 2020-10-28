system.addusers
===============

This role will add or remove users.
Upon creating a user, the password will be expired so that the user has to change it upon first login.
Depending on the variable ssh_key_etc, the public keys will be installed in /etc/ssh/authorized_keys

Requirements
------------

Just make sure Ansible has access to the target host(s).

Example Playbook
----------------

    - hosts: all
      roles:
        - system.addusers
      vars:
        server_cluster:
          john:
            state: "present"
            name: "john"
            admin: "true"
            uid: 1000
            groups:
            pass_hash: "$6$SOMELONGHASHHERE"
            public_key: |
              ssh-rsa SOMERSAKEY comment
              ssh-ed25519 SOMEOTHERKEY comment
            shell: "/bin/zsh"
          jane:
            state: "present"
            name: "jane"
            admin: "false"
            uid: 1001
            groups: "developers"
            public_key: |
              ssh-rsa SOMERSAKEY comment
              ssh-ed25519 SOMEOTHERKEY comment
            shell: "/bin/bash"
TODO
----

- Add option to set password hash (and thus not expire password)
- Add option to set AuthorizedKeysFile to /etc/ssh/authorized_keys/%u in sshd_config

License
-------

BSD

Author
------
Peter Tambach, info@petertambach.com

