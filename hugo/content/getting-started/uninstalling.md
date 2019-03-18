---
title: "Uninstalling"
date:
draft: false
weight: 90
---

# Uninstalling PostgreSQL Operator

The following assumes the proper [prerequisites are satisfied](/getting-started/prerequisites)
we can now deprovision the PostgreSQL Operator.

First, it is recommended to use the playbooks tagged with the same version
of the PostgreSQL Operator currently deployed.

With the correct playbooks acquired and prerequisites satisfied, simply run
the following command:

```bash
ansible-playbook -i /path/to/inventory main.yml --tags=deprovision
```

## Deleting `pgo` Client

The `pgo` client is not installed as part of the playbook workflow.  It is required to
delete `pgo` manually.
