Role Name
=========

This role install InfluxDB higher than 1.2.0

Requirements
------------

Ubuntu & Ansible V2.1

Role Variables
--------------

### InfluxDB Task

    ansible-influxdb :
        - influxdb_install.yml
        - influxdb_lv.yml
        - influxdb_config.yml
        - influxdb_bdd.yml
        - influxdb_user.yml
        - influxdb_privilege.yml
        - influxdb_retention_policies.yml

### Variables

    # secrets
    influxdb_admin_password: < password_admin_user >
    influxdb_password_user: < password_user >

    # Default variable

    # Base
    influxdb_version: latest
    influxdb_lv: True
    influxdb_vg_name: vg_vroot
    influxdb_lv_name: lv_influxdb
    influxdb_lvsize: 5
    influxdb_service_name: influxdb
    influxdb_conf_path: /etc/influxdb/
    influxdb_data_path: /var/lib/influxdb/

    # HTTP auth
    influxdb_http: True
    influxdb_http_auth: True
    influxdb_http_port: 8086
    influxdb_bind_address_http: ""

    # User admin
    influxdb_admin_user: root

    # Port & Bind
    influxdb_meta_port: 8088
    influxdb_bind_address_meta: ""

    # Database
    influxdb_create_database: False
    influxdb_db_name_collectd: < database name >
    influxdb_db_name_graphite: < database name >

    # User
    influxdb_create_user: False
    influxdb_user_name: < user name >

    # Retention policies
    influxdb_retention_days: 7
    influxdb_replica_factor: 1

    # Collectd
    influxdb_collectd_input: False
    influxdb_collectd_bind: :25826
    influxdb_collectd_typesdb: /usr/share/collectd/types.db

    # Graphite
    influxdb_collectd_input: False
    influxdb_collectd_bind: :2003

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
Note: The group must be named "hosts" in inventory file

Inventory file example:

    [hosts]
    host01.btsys.local
    host02.btsys.local
    host03.btsys.local

Playbook example:

    - name: deploy influxdb
      hosts: hosts
      become: yes
      vars_files:
        - secret.yml
      vars:
        - influxdb_create_database: True
        - influxdb_db_name: < Database name >
        - influxdb_create_user: True
        - influxdb_user_name: < User name >
      roles:
        - ../ansible-influxdb

Tags
-----------------

    installation : Influxdb install

Exemple of launch
-----------------

      export ANSIBLE_HOST_KEY_CHECKING=False; ansible-playbook -i hosts playbook.yml --ask-vault-pass --ask-pass --ask-become-pass --tags installation

License
-------

BSD

Author Information
------------------

BSO ISL - sponge
