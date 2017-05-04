# UCLALib Ansible Role: Fedora Camel

Ansible role to install the Fedora Camel Toolset into an Apache Karaf OSGi container

## Dependencies
* uclalib_role_java
* uclalib_role_karaf

## Variables
* `fc_tools_version` - Defines the version of the Fedora Camel Toolbox to install

* `karaf_fctools_repoadd` - Defines the Fedora Camel feature repository to add to Apache Karaf

* `fedora_username` - Defines the username that has access to the Fedora installation

* `fedora_password` - Defines the password associated with the fedora username

* `fedora_url` - Defines URL to the Fedora repository server

* `solr_url` - Defines URL to the solr instance instance used by the Fedora repository

* `karaf_fctools_install` - variable that instantiates the list Fedora Camel Toolbox features

  * `feature` - Defines the Fedora Camel Toolbox feature name

  * `config` - Defines the Fedora Camel Toolbox config file for the feature

## Example Usage in a play

```
---
- name: uclalib_fedoracamel.yml
  become: yes
  become_method: sudo
  hosts: karaf4
  vars_files:
    - vars/fctools_vars.yml
  vars:
    fedora_url: "fedora_server.library.ucla.edu"
    solr_url: "solr_server.library.ucla.edu/solr/fedora4"
    karaf_fctools_install:
      - feature: "fcrepo-indexing-solr"
        config: "org.fcrepo.camel.indexing.solr.cfg"
      - feature: "fcrepo-fixity"
        config: "org.fcrepo.camel.fixity.cfg"
      - feature: "fcrepo-serialization"
        config: "org.fcrepo.camel.serialization.cfg"
      - feature: "fcrepo-reindexing"
        config: "org.fcrepo.camel.reindexing.cfg"
      - feature: "camel-saxon"

  roles:
    - { role: uclalib_role_java }
    - { role: uclalib_role_karaf }
    - { role: uclalib_role_fedoracamel }
```
The var/fctools_vars.yml file could be an Ansible Vault encrypted file containing the fedora username and password. 
