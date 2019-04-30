egeneralov.zabbix-userparameter-postgresql
==========================================

Provision zabbix monitoring for postgresql

Requirements
------------

Supported debian-based os.

Role Variables
--------------

Variables from roles. New changes is added userparameter and create extension for databases.

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
