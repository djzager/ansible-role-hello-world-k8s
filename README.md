Ansible Role: Hello World Kubernetes
======================

[![Build Status](https://travis-ci.org/djzager/ansible-role-hello-world-k8s.svg?branch=master)](https://travis-ci.org/djzager/ansible-role-hello-world-k8s)

Manages a Hello World application in Kubernetes|OpenShift. This project also
includes the necessary bits for deploying this role as an Operator in a
Kubernetes|OpenShift cluster.

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
`my-hello-world-namespace` namespace.

```
- hosts: localhost
  vars:
    name: my-hello-world
    namespace: my-hello-world-namespace
    size: 3
  roles:
    - djzager.hello_world_k8s
```

# Example Operator

**NOTE** The example below assumes that you are essentially a cluster admin for
the Kubernetes|OpenShift cluster. This is because you'll be creating a Role,
Service Accounts Role Binding, and a Custom Resource Definition.

First, we build our operator using `operator-sdk`, link
[here](https://github.com/operator-framework/operator-sdk/):

```
$ operator-sdk build hello-world-operator
```

Then, we create the important objects our operator needs to run:

```
$ kubectl create -f deploy/service_account.yaml \
               -f deploy/role.yaml \
               -f deploy/role_binding.yaml \
               -f deploy/crds/examples_v1alpha1_helloworld_crd.yaml
```

Then, we start the operator:

```
# Use the image name from the operator-sdk build step above
# and set the imagePullPolicy to Never
$ sed 's|REPLACE_IMAGE|hello-world-operator|g; s|Always|Never|' deploy/operator.yaml | kubectl create -f -
```

Finally, create a HelloWorld resource:

```
$ kubectl create -f deploy/crds/examples_v1alpha1_helloworld_cr.yaml
```
