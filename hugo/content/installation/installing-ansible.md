---
title: "Installing Ansible"
date:
draft: false
weight: 30
---

## Installing Ansible on Linux or MacOS

To install Ansible on Linux or MacOS, [see the official documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-the-control-machine)
 provided by Ansible.

## Installing Ansible on Windows (Ubuntu Subsystem)

## Install Google Cloud SDK (Optional)

If Crunchy PostgreSQL Operator is going to be installed in a Google Kubernetes 
Environment the Google Cloud SDK is required.

To install the Google Cloud SDK on Linux or MacOS, see the 
[official Google Cloud documentation](https://cloud.google.com/sdk/install).

When installing the Google Cloud SDK on the Windows Ubuntu Subsystem, run the following 
commands to install:

```bash
wget https://sdk.cloud.google.com --output-document=/tmp/install-gsdk.sh
# Review the /tmp/install-gsdk.sh prior to running
chmod +x /tmp/install-gsdk.sh
/tmp/install-gsdk.sh
```
