# Ansible Role: CBX Backends Elasticsearch

## Description

Role to configure elasticsearch

## Requirements

- Ansible >= 2.9 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| es_version | 5.6.16 | Version to be installed
| max_clause_count | 10240 | |
| CLUSTER_PROJECT | NONE | Cluster project name, fail if empty |
| CLOUD_PROVIDER | NONE | Cloud provider to install cluster, fail if empty |

## Relation between `cbx.backends.elasticsearch` and cbx stack deployment

`cbx.backends.elasticsearch` role will configure Elasticsearch for CBX stack specifics

## Example

### Playbook

```yaml
---
- name: Playbook to install Elasticsearch
  hosts: elasticsearch
  become: true

  vars_files: "{{ lookup('env','PWD') }}/backends.credentials"

  vars:
    elasticsearch_username: "{{ elasticsearch_cbxapp.user }}"
    elasticsearch_password: "{{ elasticsearch_cbxapp.pass }}"
    elasticsearch_username1: "{{ elasticsearch_developer.user }}"
    elasticsearch_password1: "{{ elasticsearch_developer.pass }}"

  roles:
    - cbx.backends.elasticsearch
```

### Run

```shell
ansible-playbook ansible-automation/playbook_cbx_backends_elasticsearch.yml \
  -i cbx-backends-inv.properties \
  -e cluster_project=mycluster01 \
  -e cloud_provider=ibm
```

## License
BSD

## Author Information

Joao Santos (joao.santos@intellectdesign.com)  
Ported from [openshift-origin-aws](https://bitbucket.org/igtbdigital/openshift-origin-aws) credits to:
* Robin Huiser (robin.huiser@intellectdesign.com)
* Rui Teles (rui.teles@intellectdesign.com)
