---
title: "Installing Ansible"
date:
draft: false
weight: 30
---

## Installing Ansible on Linux or MacOS

To install Ansible on Linux or MacOS, [see the official documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-the-control-machine)
 provided by Ansible.

## Installing Ansible on Windows (Cygwin)

The following instructions will install [Cygwin](https://www.cygwin.com/) with Ansible.

First the Cygwin [installer must be downloaded](http://cygwin.com/setup-x86_64.exe).  This 
should only be downloaded and not executed.

Next, open a Windows Command Prompt using the following:

* `[WINDOWS KEY] + R`
* Type into the run prompt `cmd` and press enter

With the Windows Command Prompt open, paste the following command into the prompt:

```
%HOMEPATH%\Downloads\setup-x86_64.exe ^
--site http://cygwin.mirror.constant.com ^
--quiet-mode ^
--arch x86 ^
--verbose ^
--packages binutils,curl,cygwin32-gcc-g++,gcc-g++,git,gmp,libffi-devel,libgmp-devel,libsodium-devel,make,nano,openssh,libcrypt-devel,openssl,openssl-devel,python36,python36-pip,python36-setuptools,python36-devel,python36-crypto,python36-cryptography,vim,unzip,wget
```

### Setting Up Cygwin Environment

Once the installation is complete navigate to the desktop and double click the Cygwin shortcut icon.

After launching the Cygwin terminal we can tune `~/.bashrc` by running the following commands:

```
cat <<EOF >> ~/.bashrc
PS1='\[\e[32m\]\u@\h:\W> \[\e[0m\]'
TERM=cygwin
export PS1
export TERM
EOF
```

Apply those changes to the current session by running:

```bash
source ~/.bashrc
```

### Install Ansible in Cygwin

Next, run the following command to install Ansible (this will take some time):

```bash
pip3.6 install ansible
```

### Install `kubectl` in Cygwin

If the Crunchy PostgreSQL Operator will be deployed to a Kubernetes cluster, we 
will require `kubectl`

To download `kubectl` run the following commands:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/windows/amd64/kubectl.exe
mv ./kubectl.exe /usr/local/bin/kubectl
chmod +x /usr/local/bin/kubectl
```

### Install `oc` in Cygwin

If the Crunchy PostgreSQL Operator will be deployed to an OpenShift cluster, we
will require `oc`

To download `oc` run the following commands:

```bash
curl -LO https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-windows.zip
unzip openshift-origin-client-tools-v3.11.0-0cbc58b-windows.zip
mv ./oc.exe /usr/local/bin/oc
chmod +x /usr/local/bin/oc
```
