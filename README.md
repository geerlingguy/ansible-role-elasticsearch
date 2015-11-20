# Ansible Role: Elasticsearch

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch)

An Ansible Role that installs Elasticsearch on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see vars/main.yml):

```
es_network_host: localhost
```

Elasticsearch `network.host`
[Setting](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-network.html).

To listen to multiple interfaces, e.g. on eth1 and localhost, use the
array syntax and escape the quotes:

```
  roles:
    - { role: geerlingguy.elasticsearch, es_network_host: '[\"_eth1:ipv4_\", \"localhost\"]' }
```

## Dependencies

  - geerlingguy.java

## Example Playbook

    - hosts: search
      roles:
        - { role: geerlingguy.java }
        - { role: geerlingguy.elasticsearch }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
