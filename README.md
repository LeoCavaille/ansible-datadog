Ansible Datadog Role
========

Install and configure Datadog base agent & checks.


Role Variables
--------------

- `datadog_api_key` - Needs to be defined. Your Datadog API key.
- `datadog_checks` - YAML configuration for agent checks to drop into `/etc/dd-agent/conf.d`.
- `datadog_config` - Settings to place in `/etc/dd-agent/datadog.conf`.

Dependencies
------------
None

Example Playbooks
-------------------------
```
- hosts: servers
  roles:
    - dustinbrown.datadog
  vars:
    datadog_api_key: "123456"
    datadog_config:
      tags: "mytag0, mytag1"
      log_level: INFO
    datadog_checks:
      ssh_check:
        init_config:
        instances:
          - host: localhost
            port: 22
            username: root
            password: changeme
            sftp_check: True
            private_key_file:
            add_missing_keys: True
      nginx:
        init_config:
        instances:
          - nginx_status_url: http://example.com/nginx_status/
            tags:
              - instance:foo
          - nginx_status_url: http://example2.com:1234/nginx_status/
            tags:
              - instance:bar
```

```
- hosts: servers
  roles:
    - { role: dustinbrown.datadog, datadog_api_key: "mykey" }
```

License
-------

Apache2

Author Information
------------------

brian@akins.org
dustinjamesbrown@gmail.com --Forked from brian@akins.org
