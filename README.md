email
=========

No bells and whistles email, plain Dovecot and Exim4 setup for Debian boxes.

Role Variables
--------------

- `email_server_external_ip`
- `email_users`: Dictionary with `user` and `password` keys.
- `email_domain_zone`: Your domain (eg: foo.com)
- `email_domain_ns_provider`: Only cloudflare is supported (Default: `cloudflare`)
- `cloudflare`: Dictionary with `email` and `api_key` keys.

Dependencies
------------

- `geerlingguy.certbot`

Example Playbook
----------------

    - hosts: foo
      become: yes
      gather_facts: yes
      roles:
        - name: email
          vars:
            email_server_external_ip: 192.168.1.1
            email_users:
              - name: foo
                password: bar
            email_domain_zone: foo.bar
            cloudflare:
              email: foo@bar.com
              api_key: bar

SMTP/IMAP connection details
----------------------------

- email: `foo@foo.bar`
- server: `smtp.foo.bar`/`imap.foo.bar`
- username: `foo`
- password: `bar`
- `STARTTLS`

License
-------

BSD-3-Clause
