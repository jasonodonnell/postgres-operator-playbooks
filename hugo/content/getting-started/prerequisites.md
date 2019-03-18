---
title: "Prerequisites"
date:
draft: false
weight: 40
---

# Prerequisites

The following is required prior to installing PostgreSQL Operator using Ansible:

* Ansible 2.4.6+
* Kubernetes v1.11+ or OpenShift v3.09+
* `kubectl` or `oc` configured to communicate with Kubernetes

## Configuring the Inventory File

The `inventory` file included with the PostgreSQL Operator Playbooks allows installers 
to configure how the operator will function when deployed into Kubernetes.  This file 
should contain all configurable variables the playbooks offer.

The following are the variables available for configuration:

| Name                              | Default     | Description                                                                                                                                                                      |
|-----------------------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `archive_mode`                    | true        | Set to true enable archive logging on all newly created clusters.                                                                                                                |
| `archive_timeout`                 | 60          | Set to a value in seconds to configure the timeout threshold for archiving.                                                                                                      |
| `auto_failover_replace_replica`   | false       | Set to true to replace promoted replicas during failovers with a new replica on all newly created clusters.                                                                      |
| `auto_failover_sleep_secs`        | 9           | Set to a value in seconds to configure the sleep time before initiating a failover on all newly created clusters.                                                                |
| `auto_failover`                   |  false      | Set to true enable auto failover capabilities on all newly created clusters.                                                                                                     |
| `backrest_storage`                | storage1    | Set to configure which storage definition to use when creating volumes used by pgBackRest on all newly created clusters.                                                         |
| `backrest`                        | false       | Set to true enable pgBackRest capabilities on all newly created clusters.                                                                                                        |
| `backup_storage`                  | storage1    | Set to configure which storage definition to use when creating volumes used by pgBaseBackup on all newly created clusters.                                                       |
| `badger`                          | false       | Set to true enable pgBadger capabilities on all newly created clusters.                                                                                                          |
| `ccp_image_prefix`                | crunchydata | Configures the image prefix used when creating containers from Crunchy Container Suite.                                                                                          |
| `ccp_image_tag`                   |             | Configures the image tag (version) used when creating containers from Crunchy Container Suite.                                                                                   |
| `cleanup`                         | false       | Set to configure the playbooks to delete all objects when deprovisioning Operator.  Note: this will delete all objects related to the Operator (including clusters provisioned). |
| `co_image_prefix`                 | crunchydata | Configures the image prefix used when creating containers for the Crunchy PostgreSQL Operator (apiserver, operator, scheduler..etc).                                             |
| `co_image_tag`                    |             | Configures the image tag used when creating containers for the Crunchy PostgreSQL Operator (apiserver, operator, scheduler..etc)                                                 |
| `crunchy_debug`                   | false       | Set to configure Operator to use debugging mode.  Note: this can cause sensitive data such as passwords to appear in Operator logs.                                              |
| `db_name`                         | userdb      | Set to a value to configure the default database name on all newly created clusters.                                                                                             |
| `db_password_age_days`            | 60          | Set to a value in days to configure the expiration age on PostgreSQL role passwords on all newly created clusters.                                                               |
| `db_password_length`              | 20          | Set to configure the size of passwords generated by the operator on all newly created roles.                                                                                     |
| `db_port`                         | 5432        | Set to configure the default port used on all newly created clusters.                                                                                                            |
| `db_replicas`                     | 1           | Set to configure the amount of replicas provisioned on all newly created clusters.                                                                                               |
| `db_user`                         | testuser    | Set to configure the username of the dedicated user account on all newly created clusters.                                                                                       |
| `kubernetes_context`              |             | When deploying to Kubernetes, set to configure the context name of the kubeconfig to be used for authentication.                                                                 |
| `kubernetes_namespace`            |             | When deploying to Kubernetes, set to configure the namespace where Operator should be installed.                                                                                 |
| `log_statement`                   | none        | Set to `none`, `ddl`, `mod`, or `all` to configure the statements that will be logged in PostgreSQL's logs on all newly created clusters.                                        |
| `metrics`                         | false       | Set to true enable performance metrics on all newly created clusters.                                                                                                            |
| `openshift_host`                  |             | When deploying to OpenShift, set to configure the hostname of the OpenShift cluster to connect to.                                                                               |
| `openshift_password`              |             | When deploying to OpenShift, set to configure the password used for login.                                                                                                       |
| `openshift_project`               |             | When deploying to OpenShift, set to configure the project name where Operator should be installed.                                                                               |
| `openshift_skip_tls_verify`       |             | When deploying to Openshift, set to ignore the integrity of TLS certificates for the OpenShift cluster.                                                                          |
| `openshift_token`                 |             | When deploying to OpenShift, set to configure the token used for login (when not using username/password authentication).                                                        |
| `openshift_user`                  |             | When deploying to OpenShift, set to configure the username used for login.                                                                                                       |
| `pgo_password`                    |             | Configures the pgo administrator password.                                                                                                                                       |
| `pgo_username`                    | admin       | Configures the pgo administrator username.                                                                                                                                       |
| `primary_storage`                 | storage2    | Set to configure which storage definition to use when creating volumes used by PostgreSQL primaries on all newly created clusters.                                               |
| `replica_storage`                 | storage3    | Set to configure which storage definition to use when creating volumes used by PostgreSQL replicas on all newly created clusters.                                                |
| `scheduler_timeout`               | 3600        | Set to a value in seconds to configure the `pgo-scheduler` timeout threshold when waiting for schedules to complete.                                                             |
| `service_type     `               | ClusterIP   | Set to configure the type of Kubernetes service provisioned on all newly created clusters.                                                                                       |
| `storage<ID>_access_mode`         |             | Set to configure the access mode of the volumes created when using this storage definition.                                                                                      |
| `storage<ID>_class`               |             | Set to configure the storage class name used when creating dynamic volumes.                                                                                                      |
| `storage<ID>_fs_group`            |             | Set to configure any filesystem groups that should be added to security contexts on newly created clusters.                                                                      |
| `storage<ID>_size`                |             | Set to configure the size of the volumes created when using this storage definition.                                                                                             |
| `storage<ID>_supplemental_groups` |             | Set to configure any supplemental groups that should be added to security contexts on newly created clusters.                                                                    |
| `storage<ID>_type`                |             | Set to either `create` or `dynamic` to configure the operator to create persistent volumes or have them created dynamically by a storage class.                                  |
| `xlog_storage`                    | storage1    | Set to configure which storage definition to use when creating volumes used to store Write Ahead Logs (WAL) archives on all newly created clusters.                              |

## Storage

Kubernetes and OpenShift offer support for a variety of storage types.  The Crunchy 
PostgreSQL Operator must be configured to utilize the storage options available by 
configuring the `storage` options included in the inventory file.

{{% notice tip %}}
At this time the Crunchy PostgreSQL Operator Playbooks only support storage classes.
{{% /notice %}}

### Considerations for Multi-Zone Cloud Environments

When using the Operator in a Kubernetes cluster consisting of nodes that span 
multiple zones, special consideration must betaken to ensure all pods and the 
volumes they require are scheduled and provisioned within the same zone.  Specifically,
being that a pod is unable mount a volume that is located in another zone, any 
volumes that are dynamically provisioned must be provisioned in a topology-aware 
manner according to the specific scheduling requirements for the pod. For instance, 
this means ensuring that the volume containing the database files for the primary 
database in a new PostgreSQL cluster is provisioned in the same zone as the node 
containing the PostgreSQL primary pod that will be using it.

For instructions on setting up storage classes for multi-zone environments, see 
the [PostgreSQL Operator Documentation](https://crunchydata.github.io/postgres-operator/stable/design/).

### Examples

The following are examples on configuring the storage variables for different types 
of storage classes.

#### Generic Storage Class

To setup storage1 to use a the storage class `fast`

```ini
storage1_access_mode='ReadWriteOnce'
storage1_size='10G'
storage1_type='dynamic'
storage1_class='fast'
```

To assign this storage definition to all `primary` pods created by the Operator, we 
can configure the `primary_storage=storage1` variable in the inventory file.

#### GKE

The storage class provided by Google Kubernetes Environment (GKE) can be configured 
to be used by the Operator by setting the following variables in the `inventory` file:

```ini
storage1_access_mode='ReadWriteOnce'
storage1_size='10G'
storage1_type='dynamic'
storage1_class='standard'
storage1_fs_group=26
```

To assign this storage definition to all `primary` pods created by the Operator, we 
can configure the `primary_storage=storage1` variable in the inventory file.

{{% notice tip %}}
To utitlize mutli-zone deployments, see _Considerations for Multi-Zone Cloud Environments_ above.
{{% /notice %}}
