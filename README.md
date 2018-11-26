hello-world-apb
======================

[![Build Status](https://travis-ci.org/ansibleplaybookbundle/hello-world-apb.svg?branch=master)](https://travis-ci.org/ansibleplaybookbundle/hello-world-apb)

An apb for deploying a simple [hello world](https://hub.docker.com/r/ansibleplaybookbundle/hello-world/) app that can be bound to PostgreSQL for testing purposes.

## What it does
* Deploys a web app that can be bound to a database.

## Parameters
* NAMESPACE: Optional, default 'hello-world', Namespace to deploy the cluster in.

## Running the application
```
docker run --rm --net=host \
-v $HOME/.kube:/opt/apb/.kube:z \
-u $UID \
docker.io/ansibleplaybookbundle/hello-world-apb \
provision --extra-vars 'namespace=hello-world'
```

## Tearing down the application
```
docker run --rm --net=host \
-v $HOME/.kube:/opt/apb/.kube:z \
-u $UID \
docker.io/ansibleplaybookbundle/hello-world-apb \
deprovision --extra-vars 'namespace=hello-world'
```
