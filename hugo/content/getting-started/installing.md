---
title: "Installing"
date:
draft: false
weight: 45
---

# Installing

The following assumes the proper [prerequisites are satisfied](/getting-started/prerequisites)
we can now install the PostgreSQL Operator.

## Installing on Linux

On a Linux host with Ansible installed we can run the following command to install 
the PostgreSQL Operator:.

The following command should be run from the directory where the
`postgres-operator-playbooks` project is located:

```bash
ansible-playbook -i /path/to/inventory main.yml --tags=install
```

## Installing on MacOS

On a MacOS host with Ansible installed we can run the following command to install
the PostgreSQL Operator.

The following command should be run from the directory where the
`postgres-operator-playbooks` project is located:

```bash
ansible-playbook -i /path/to/inventory main.yml --tags=install
```

## Installing on Windows

On a Windows host with a Cygwin terminal we can run the following command to install 
the PostgreSQL Operator:

The following command should be run from the directory where the
`postgres-operator-playbooks` project is located:

```bash
ansible-playbook -i /path/to/inventory main.yml --tags=install
```

## Verifying the Installation

This may take a few minutes to deploy.  To check the status of the deployment run 
the following:

```bash
# Kubernetes
kubectl get deployments -n <NAMESPACE_NAME>
kubectl get pods -n <NAMESPACE_NAME>

# OpenShift
oc get deployments -n <NAMESPACE_NAME>
oc get pods -n <NAMESPACE_NAME>
```

## Configuring `pgo`


