# Ansible Role: Elasticsearch

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-elasticsearch)

An Ansible Role that installs Elasticsearch on Debian/Ubuntu.

**Note**: This role is under active development and is not considered stable quite yet. I am working on making sure it runs across a wider variety of platforms, and also will work with different kinds of workflows you may have. Please file issues on GitHub if you find a problem!

## Requirements

None.

## Role Variables

None.

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
