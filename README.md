## OCI-RSA-ANSIBLE-KIBANA
This stack contains the Wazuh cluster Kibana Ansible playbook. This stands up the [Kibana](https://www.elastic.co/products/kibana) and [Wazuh APP](https://github.com/wazuh/wazuh-kibana-app).

## Ansible Role: Wazuh-Kibana
More information on the Wazuh-Cluster can be found [here](/wazuh-kibana/README.md).

## Ansible Role: Wazuh Ansible
We are using <b>Galaxy</b> which provides pre-packaged units of work known to Ansible as roles and collections. Content from 
roles and collections of the <b>wazuh-ansible</b> is referenced in Ansible PlayBooks. This playbook installs and 
configures Wazuh agent and manager.

## Ansible Role: OCI-RSA-Ansible-Base
More information on the oci-rsa-ansible-base can be found [here](https://bitbucket.oci.oraclecorp.com/projects/RSA/repos/oci-rsa-ansible-base).

## Requirements

- [Ansible core](https://docs.ansible.com/ansible-core/devel/index.html) >= 2.11.0
- Oracle Linux >= 7.9

Dependencies
------------

A list of other roles hosted on Galaxy:
* [geerlingguy.clamav](https://github.com/geerlingguy/ansible-role-clamav): Installs ClamAV on RedHat Linux server.
* [wazuh-ansible](https://github.com/wazuh/wazuh-ansible): These playbooks install and configure Wazuh agent, manager and 
  Elastic Stack

A list of other roles hosted on Github:
* [oci-rsa-ansible-base](https://bitbucket.oci.oraclecorp.com/projects/RSA/repos/oci-rsa-ansible-base): Installs base 
  packages and sets configuration for general security, montoring, and auditing purposes.
    
## Code style


[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](https://github.com/oracle-quickstart)
 

## Branches
* `main` branch contains the latest code.


## Usage
* Launching the playbook:
    ```
    ansible-playbook -i localhost, $OCI_RSA_BASE/${playbook_name}/main.yml --connection=local 
    ```
* General usage: 
  - This stands up the [Kibana](https://www.elastic.co/products/kibana) 
  - This stands up the  [Wazuh APP](https://github.com/wazuh/wazuh-kibana-app).
  

Example Playbook
----------------

An example of how to use the roles:
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

## Documentation

* [Wazuh Ansible documentation](https://documentation.wazuh.com/current/deploying-with-ansible/index.html)
* [Full documentation](http://documentation.wazuh.com)

## How to Contribute
Interested in contributing?  See our contribution [guidelines](CONTRIBUTE.md) for details.

## License
This repository and its contents are licensed under [UPL 1.0](LICENSE).