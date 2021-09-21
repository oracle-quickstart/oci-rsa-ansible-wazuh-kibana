Role: WAZUH-KIBANA
=========

Installs the [Open Distro Kibana](https://opendistro.github.io/for-elasticsearch-docs/docs/kibana/) 
implementation and [Wazuh App](https://github.com/wazuh/wazuh-kibana-app).

Requirements
------------

This role will work on:

- [Ansible core](https://docs.ansible.com/ansible-core/devel/index.html) >= 2.11.0
- [Oracle Autonomous Linux](https://www.oracle.com/linux/autonomous-linux/) >= 7.9

Role Variables
--------------

Overrides the cluster settings like Open Distro Kibana version to 1.13.2, Wazuh version to 4.1.5 and Open Distro Elastic
stack version to 7.10.2 .
```
kibana_opendistro_version: 1.13.2
wazuh_version: 4.1.5
elastic_stack_version: 7.10.2
```

Overrides the Kibana node settings and Kibana node network settings.
```
kibana_node_name: '{{ ansible_fqdn }}'
kibana_server_name: "kibana"
kibana_server_host: "0.0.0.0"
kibana_conf_path: /etc/kibana
kibana_server_port: "5601"
kibana_max_payload_bytes: 1048576
```

Disabling build from existing sources.
``` 
build_from_sources: false
```

Overriding Wazuh branch plugin to 4.1-7.10
```
wazuh_plugin_branch: 4.1-7.10
```

Setting the Nodejs NODE_OPTIONS.
```
node_options: --no-warnings --max-old-space-size=2048 --max-http-header-size=65536
```

Setting the url for the Wazuh application.
```
wazuh_app_url: https://packages.wazuh.com/4.x/ui/kibana/wazuh_kibana
```

Domain refers to the Wazuh subnet inside the primary VCN.
```
domain_name: 'wazuhsubnet.primaryvcn.oraclevcn.com'
```

Sets the Open Distro cluster name to "wazuh".
```
opendistro_cluster_name: wazuh
```

Setting the Open Distro ElasticSearch node http port, and the network host.
```
elasticsearch_network_host: 'elasticnode0.{{ domain_name }}'
elasticsearch_http_port: '9200'
```

Enabling security for the Open Distro Kibana implementation.
```
kibana_opendistro_security: true
```

Disabling Newsfeed and Telemetry for Kibana.
```
kibana_newsfeed_enabled: "false"
kibana_telemetry_optin: "false"
kibana_telemetry_enabled: "false"
```

The local path to store the generated certificates (Open Distro security plugin).
```
local_certs_path: "/etc/ssl/local"
```

Links to the Open Distro packages
```
package_repos:
  yum:
    opendistro:
      baseurl: 'https://packages.wazuh.com/4.x/yum/'
      gpg: 'https://packages.wazuh.com/key/GPG-KEY-WAZUH'
  apt:
    opendistro:
      baseurl: 'deb https://packages.wazuh.com/4.x/apt/ stable main'
      gpg: 'https://packages.wazuh.com/key/GPG-KEY-WAZUH'
```

Default Variables
------------

```
opendistro_admin_password: changeme
opendistro_kibana_user: kibanaserver
opendistro_kibana_password: changeme
```

```
wazuh_api_credentials:
  - id: "default"
    url: "https://wazuhmasterinstance.{{ domain_name }}"
    port: 55000
    username: "wazuh"
    password: "wazuh"
```

Setting the Wazuh API credentials and username is "wazuh". The password attribute can be overridden.
```
wazuh_api_credentials:
  - id: "default"
    url: "https://wazuhmasterinstance.{{ domain_name }}"
    port: 55000
    username: "wazuh"
    password: "{{ wazuh_password }}"
```

Dependencies
------------

None

Example Playbook
----------------

Use the oci-rsa-ansible-base role before to install the required software. An `extra-variables.yml` file can also be used 
to pass in other variables. An example of how to use the role:
```
    ---
    - hosts: all
      vars_files: 
        - ../extra-variables.yml
      roles: 
        - role: oci-rsa-ansible-base
          become: true
        - role: wazuh-kibana
          become: true
        - role: geerlingguy.clamav
          become: true
```


## License
This repository and its contents are licensed under [UPL 1.0](https://opensource.org/licenses/UPL).