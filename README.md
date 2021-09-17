# email

[![Molecule](https://github.com/someone-stole-my-name/ansible-role-email/actions/workflows/molecule.yml/badge.svg?branch=main)](https://github.com/someone-stole-my-name/ansible-role-email/actions/workflows/molecule.yml) [![License](https://badgen.net/github/license/someone-stole-my-name/ansible-role-email)](https://github.com/someone-stole-my-name/ansible-role-email/LICENSE)


No bells and whistles email, plain Dovecot and Exim4 setup for __Debian__ boxes.

- [email](#email)
  - [Role Variables](#role-variables)
  - [Requirements](#requirements)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [Compatibility](#compatibility)
  - [SMTP/IMAP connection details](#smtpimap-connection-details)
  - [License](#license)

## [Role Variables](#role-variables)

- `email_server_external_ip`
- `email_users`: Dictionary with `user` and `password` and `quota` keys. When quota is not present, there are no limits.
- `email_domain_zone`: Your domain (eg: `foo.com`).
- `email_domain_ns_provider`: Only Cloudflare is supported (Default: `cloudflare`).
- `email_certificates_path`: Dictionary with `certificate` and `key` keys. When both keys have a value, __LetsEncrypt certificates are not generated__. Your certificate should be a full chain and must be valid for the following subdomains:
  - `mail`
  - `smtp`
  - `imap`
- `cloudflare`: Dictionary with `email` and `api_key` keys, only required when `email_domain_ns_provider == cloudflare`.

## [Requirements](#requirements)

- 25 (SMTP) TCP
- 587 (SMTP) TCP
- 993 (IMAP) TCP
- 143 (IMAP) TCP

## [Dependencies](#dependencies)

- `geerlingguy.certbot`

## [Example Playbook](#example-playbook)

```yaml
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
          - name: bar
            password: foo
            quota: 256
        email_domain_zone: foo.bar
        cloudflare:
          email: foo@bar.com
          api_key: bar
```

## [Compatibility](#compatibility)

This role is tested on these container images:

|container|tags|
|---------|----|
|[jrei/systemd-debian](https://hub.docker.com/r/jrei/systemd-debian)|10|

## [SMTP/IMAP connection details](smtp-imap-connection-details)

- email: `foo@foo.bar`
- server: `smtp.foo.bar`/`imap.foo.bar`
- username: `foo`
- password: `bar`
- `STARTTLS`

## [License](#license)

BSD-3-Clause
