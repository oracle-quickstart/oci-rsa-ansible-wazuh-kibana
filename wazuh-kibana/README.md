Roles: Wazuh-Kibana
=========
An Ansible Role that installs [Kibana](https://www.elastic.co/products/kibana) and [Wazuh APP](https://github.com/wazuh/wazuh-kibana-app).

Requirements
------------
This role will work on:

- [Ansible core](https://docs.ansible.com/ansible-core/devel/index.html) >= 2.11.0
- Oracle Linux >= 7.

Role Variables
--------------
---

```
kibana_opendistro_version: 1.13.2
wazuh_version: 4.1.5
elastic_stack_version: 7.10.2
```
Overrides the cluster settings like kibana opendistro version to 1.13.2, wazuh version to 4.1.5 and elastic stack version
to 7.10.2 


```
kibana_node_name: '{{ ansible_fqdn }}'
kibana_server_name: "kibana"
kibana_server_host: "0.0.0.0"
kibana_conf_path: /etc/kibana
kibana_server_port: "5601"
kibana_max_payload_bytes: 1048576
```
Overrides the cluster settings like kibana node settings

``` 
build_from_sources: false
```
Disabling build from existing sources

```
wazuh_plugin_branch: 4.1-7.10
```
Overriding wazuh branch plugin to 4.1-7.10

```
node_options: --no-warnings --max-old-space-size=2048 --max-http-header-size=65536
```
Setting the Nodejs NODE_OPTIONS
```
wazuh_app_url: https://packages.wazuh.com/4.x/ui/kibana/wazuh_kibana
```
Setting the url for the wazuh application

```
domain_name: 'wazuhsubnet.primaryvcn.oraclevcn.com'
```
Domain refers to the Wazuh subnet inside the primary VCN
```
opendistro_cluster_name: wazuh
```
Sets the OpenDistro cluster name to "wazuh"

```
elasticsearch_network_host: 'elasticnode0.{{ domain_name }}'
elasticsearch_http_port: '9200'
```
Setting the elastic search node http port and the network host.

```
kibana_opendistro_security: true
kibana_newsfeed_enabled: "false"
kibana_telemetry_optin: "false"
kibana_telemetry_enabled: "false"
```


```
local_certs_path: "/etc/ssl/local"
```
The local path to store the generated certificates (OpenDistro security plugin)

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
Links to the OpenDistro packages


```
wazuh_api_credentials:
  - id: "default"
    url: "https://wazuhmasterinstance.{{ domain_name }}"
    port: 55000
    username: "wazuh"
    password: "{{ wazuh_password }}"
```
Setting the Wazuh API credentials, username is "wazuh" 


Dependencies
------------
None.

Example Playbook
----------------

An example of how to use the roles:

    ---
    - hosts: all
      roles:
        - role: wazuh-kibana
          become: true


## How to Contribute
Interested in contributing?  See our contribution [guidelines](CONTRIBUTE.md) for details.

## License
This repository and its contents are licensed under [UPL 1.0](https://opensource.org/licenses/UPL).