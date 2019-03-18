---
title: "Upgrading"
date:
draft: false
weight: 80
---

# Upgrading the PostgreSQL Operator

The following assumes the proper [prerequisites are satisfied](/getting-started/prerequisites)
we can now upgrade the PostgreSQL Operator.

First, it is recommended to use the playbooks tagged with the same version 
of the PostgreSQL Operator we will be upgrading to.

With the correct playbooks acquired and prerequisites satisfied, simply run 
the following command:

```bash
ansible-playbook -i /path/to/inventory main.yml --tags=upgrade
```

## Upgrading `pgo` Client

The `pgo` client is not installed as part of the playbook workflow.  It is required to 
install `pgo` manually.  

To obtain `pgo` [see the official releases](https://github.com/CrunchyData/postgres-operator/releases).

The new `pgo` binary should replace any existing `pgo` client tools and require no 
other configuration.
