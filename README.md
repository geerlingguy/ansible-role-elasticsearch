# Ansible Role: Elasticsearch

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch)

An Ansible Role that installs Elasticsearch on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

`elasticsearch_version`: Specify a version number to install. Default is blank, which installs the latest available version
`elasticsearch_repo_version`: Specify the repository version to use. Default is `2.x`.

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
