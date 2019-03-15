# Crunchy Data PostgreSQL Operator Playbook

<p align="center">
  <img src="crunchy_logo.png?raw=false" alt="Mr. Crunchy" width="150"/>
</p>

Latest Release: 3.5.0

## General

This repository contains Ansible Roles for deploying the Crunchy PostgreSQL Operator 
for Kubernetes and OpenShift.

## Installation

The following are required for installation using these roles:

* Ansible 2.4.6+
* [PostgreSQL Operator Client](https://github.com/CrunchyData/postgres-operator/releases) (pgo) installed.
* PostgreSQL Operator Docker Images
  * CentOS7 images can be found in Docker Hub, RHEL7 images are available to Crunchy customers

Next, edit the `inventory` file included to configure the Crunchy PostgreSQL Operator installation.

Once the `inventory` file has been configured, run the following command to deploy:

```bash
ansible-playbook -i inventory main.yml --tags="install"
```

After installation completes, set the following environment variables for `pgo` to work correctly:

```bash
export PGOUSER=~/.pgouser
export PGO_CA_CERT=/tmp/pgo-config/pg-operator.crt
export PGO_CLIENT_CERT=/tmp/pgo-config/pg-operator.crt
export PGO_CLIENT_KEY=/tmp/pgo-config/privkey.pem
export URL=$(kubectl get service postgres-operator -o=jsonpath="{.spec.clusterIP}")
export CO_APISERVER_URL=https://${URL?}:8443
```

Finally, test `pgo` is communicating with the PostgreSQL Operator API Service:

```bash
pgo version
```

## Upgrading

To upgrade PostgreSQL Operator, first update the `inventory` file with the new target 
version of PostgreSQL Operator and Crunchy Container container images to use.

Next, run the following command with the `upgrade` tag:

```bash
# NOTE: This is delete all operator related objects
ansible-playbook -i inventory main.yml --tags="upgrade"
```

## Deprovisioning

To completely remove PostgreSQL Operator, run the following command:

```bash
# NOTE: This is delete all operator related objects
ansible-playbook -i inventory main.yml --tags="deprovision"
```

## More Information

Please view the official [Crunchy Data PostgreSQL Operator documentation](https://crunchydata.github.io/postgres-operator).
