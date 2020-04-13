# Supplemental Documentation for Geerlingguy's Role

## Adding Variables to Inventory

Geerlingguy assumes an elasticsearch instance of only a single host. We need more, an infinite amount more. We need to account for the addressing of masters, data-only, and other ES-specific node types. One way to do it is through the inventory file.

The idea is, the inventory file would contain the required variables specific to each node, which are then interpolated by the `jinja2` engine at run time. 

```ini
# Elasticsearch Master nodes
[master]
192.168.60.4 es_node_name="master1"
192.168.60.5 es_node_name="master2"
192.168.60.6 es_node_name="master3"

# Elasticsearch Data only nodes
[data]
192.168.60.7 es_node_name="data1"
192.168.60.8 es_node_name="data2"
192.168.60.9 es_node_name="data3"

# All ES nodes
[multi:children]
master
data

# Master only variables
[master:vars]
elasticsearch_master_nodes='["192.168.60.4","192.168.60.5","192.168.60.6"]

# Variables applied to all hosts
[multi:vars]
ansible_ssh_user=vagrant
ansible_ssh_vagrant_private_key_file=~/.vagrant/insecure_private_key
```

The within the `Jinja2` template refer to the variables with the **mustache** syntax, `{{ var_name }}`.

Here's a simple playbook to check the variables

```yaml
---
- hosts: master
  gather_facts: no
  tasks:
  - name: Print play_hosts
    debug: 
      msg: "{{ play_hosts }}"
    run_once: yes
  - name: Dump inventory var
    debug: 
      msg: 'My list of hosts {{ elasticsearch_master_nodes }}'
    run_once: yes
  - name: Show Host and ES node name
    debug:
      msg: "ES Node Name is {{ es_node_name }}"
```

### Safety Tip

When adding multiple variables to a host in the inventory file, they are **space** separated.

```ini
[app]
192.168.60.4 es_node_name="master1" es_master_flag="true" es_data_flag="true"
192.168.60.5 es_node_name="master2" es_master_flag="true" es_data_flag="true"
```

## All Inventory Vars

| Elasticsearch.yml Param | Jinja2 Var | Inventory Var or defaults.yml |
| ----------------------- | ---------- | ------------- |
| cluster.name | elasticsearch_cluster_name | "teamconnect" | 
| node.name | elasticsearch_node_name | es_node_name |
| network.host | elasticsearch_network_host | {{ansible_default_ipv4 }} |
| node.master | elasticsearch_master_flag | es_master_flag |
| node.data | elasticsearch_data_flag | es_data_flag |
| discover.seed_hosts | elasticsearch_discovery_seed_hosts | es_seed_hosts |
| cluster.initial_master_nodes | elasticsearch_cluster_initial_master_nodes |es_initial_masters |
| path.data | elasticsearch_path_data | "/var/lib/elasticsearch" |
| path.logs | elasticsearch_path_logs | "/var/log/elasticsearch" |
