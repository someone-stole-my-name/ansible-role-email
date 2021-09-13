# email

[![Molecule](https://github.com/someone-stole-my-name/ansible-role-email/actions/workflows/molecule.yml/badge.svg?branch=main)](https://github.com/someone-stole-my-name/ansible-role-email/actions/workflows/molecule.yml) [![License](https://badgen.net/github/license/someone-stole-my-name/ansible-role-email)](https://github.com/someone-stole-my-name/ansible-role-email/LICENSE)


No bells and whistles email, plain Dovecot and Exim4 setup for __Debian__ boxes.

## Role Variables

- `email_server_external_ip`
- `email_users`: Dictionary with `user` and `password` keys.
- `email_domain_zone`: Your domain (eg: `foo.com`).
- `email_domain_ns_provider`: Only Cloudflare is supported (Default: `cloudflare`).
- `email_certificates_path`: Dictionary with `certificate` and `key` keys. When both keys have a value, __LetsEncrypt certificates are not generated__. Your certificate should be a full chain and must be valid for the following subdomains:
  - `mail`
  - `smtp`
  - `imap`
- `cloudflare`: Dictionary with `email` and `api_key` keys, only required when `email_domain_ns_provider == cloudflare`.

## Dependencies

- `geerlingguy.certbot`

## Example Playbook

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

## [Compatibility](#compatibility)

This role is tested on these container images:

|container|tags|
|---------|----|
|[jrei/systemd-debian](https://hub.docker.com/r/jrei/systemd-debian)|10|

## SMTP/IMAP connection details

- email: `foo@foo.bar`
- server: `smtp.foo.bar`/`imap.foo.bar`
- username: `foo`
- password: `bar`
- `STARTTLS`

## License

BSD-3-Clause
