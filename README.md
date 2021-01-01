Role Name
=========

A role to install `Elasticsearch` cluster. (currently supports only `Debian`)

Requirements
------------

`Elasticsearch` requires `Java`. if `Java` is installed on the hosts, specify it's location via `java_home` environment variable. Otherwise, `chubock.java` role which this role declares a dependency on will install `java` at `java_home` location. for more information about `chubock.java` visit [ansible-role-java](https://github.com/chubock/ansible-role-java). 

Role Variables
--------------

Variables defined in vars/main.yml are:

    es_data_path: sets path.data elasticsearch config property. default: /var/lib/elasticsearch
    es_log_path: sets path.logs elasticsearch config property. default: /var/log/elasticsearch
    es_network_host: sets network.host elasticsearch config property. default: ["_local_", "_site_"]
    
Other variables defined in defaults/main.yml are:

    es_config_template: path to template for elasticsearch.yml config file, enabling users to use their own version of configuration file for elasticsearch. default: elasticsearch.yml.j2
    es_cluster_name: sets cluster.name elasticsearch config property. default: elasticsearch
    es_node_name: sets node.name elasticsearch config property. default: "{{inventory_hostname}}"
    es_node_master: sets node.master elasticsearch config property. default: true
    
    stable_rolling_update: indicates whether to wait for the culster state to became green or not. default: true
    stable_rolling_update_retries: number of retries for getting cluster state. default: 24
    stable_rolling_update_delay: seconds to wait after each retry to get the cluster state. default: 5

    elasticsearch_exporter: indicates whether to install prometheus exporter for elasticsearch or not. default: true
    elasticsearch_exporter_home: path to install prometheus elasticsearch exporter. default: /var/lib/prometheus
    
    elasticsearch_hosts: sets cluster.initial_master_nodes & discovery.seed_hosts elasticsearch config properties. default: "{{ ansible_play_hosts }}"
    es_cluster_initial_master_nodes: sets cluster.initial_master_nodes config property. default: "{{ elasticsearch_hosts }}"
    es_discovery_seed_hosts: sets discovery.seed_hosts elasticsearch config property. default: "{{ elasticsearch_hosts }}"
    
Note that, if proxy_url variable is set, then tries to install `Elasticsearch` through proxy.

Dependencies
------------

Depends on `chubock.java` role. for more information about `chubock.java` visit [ansible-role-java](https://github.com/chubock/ansible-role-java).

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: elasticsearch
      roles:
         - { role: chubock.elasticsearch, es_cluster_name: dev, stable_rolling_update: false }

License
-------

Apache-2
