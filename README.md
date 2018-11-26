Ansible Role: Hello World Kubernetes
======================

[![Build Status](https://travis-ci.org/djzager/ansible-role-hello-world-k8s.svg?branch=master)](https://travis-ci.org/djzager/ansible-role-hello-world-k8s)

Manages a Hello World application in Kubernetes|OpenShift.

# Requirements

* ansible >= 2.6
* [openshift python package](https://pypi.org/project/openshift/)

# Role Variables

See [defaults/main.yml](defaults/main.yml).

# Dependencies

None

# Example Playbook

**NOTE** The example below assumes that you have a running Kubernetes|OpenShift
cluster and that you have sufficient permissions in the
`my-not-so-secret-namespace` namespace.

```
- hosts: localhost
  vars:
    name: my-hello-world
    namespace: my-not-so-secret-namespace
    size: 3
  roles:
    - djzager.hello-world-k8s
```
