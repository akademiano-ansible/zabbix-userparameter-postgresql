egeneralov.zabbix-userparameter-postgresql
==========================================

Provision zabbix monitoring for postgresql. Will be added userparameter and create extension for each database.

Note: will be used `delegate_to: localhost`, so packages installation from `requirements.txt` is mandatory.

Requirements
------------

Debian-based OS

Role Variables
--------------

- **zbx_server_url**: `http://127.0.0.1`
- **zbx_login_user**: `Admin`
- **zbx_login_password**: `zabbix`
- **zbx_template_name**: `PostgreSQL Simple Template`

Also see variables from other roles.

Dependencies
------------

- [egeneralov.postgresql-repository](https://github.com/egeneralov/postgresql-repository)
- [egeneralov.postgresql](https://github.com/egeneralov/postgresql)
- [egeneralov.zabbix-agent](https://github.com/egeneralov/zabbix-agent)

Example Playbook
----------------

    ---
    - hosts: postgresql-servers
      vars:

        zbx_server_url: http://zbx.company.tld
        zbx_login_user: Admin
        zbx_login_password: zabbix
        zbx_template_name: PostgreSQL Simple Template

        zbx_version: 4.2
        zabbix_server: zabbix.company.tld
        
        pgdg_version: 9.6
        pgdg_users:
          - user: root
            password: root
            database: root
          - user: django
            password: django
            database: django
        
        pgdg_pg_hba_conf:
          - {
              "connection_type": "host",
              "database": "all",
              "user": "all",
              "address": "127.0.0.1/32",
              "method": "md5"
            }

        pgdg_postgresql_conf:
          - { "k": "listen_addresses", "v": "'127.0.0.1'" }
          - { "k": "port", "v": "5432" }

      roles:
        - egeneralov.zabbix-userparameter-postgresql

License
-------

MIT

Author Information
------------------

Eduard Generalov <eduard@generalov.net>
