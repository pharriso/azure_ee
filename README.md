Ansible Azure EE example
=========

This repo contains an execution environment definition for automating against Azure.

Requirements
------------

* A pre-deployed RHEL8 instance.

Installing ansible-builder
------------

Follow the official [docs to install ansible-builder](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/ansible_builder_guide/assembly-using-builder).

**Note** the bundled installer includes the RPMS. Enable the local repository in **/etc/yum.repos.d/ansible-automation-platform.repo** and install ansible-builder with yum/dnf.

Getting the Azure python dependencies
------------

Install the version of the azure.azcollection collection that you want to use. For example:

```bash
ansible-galaxy collection install azure.azcollection:azure.1.13.0 --force
```

The collection provides the list of python dependencies that you need. You can use this list to replace requirements.txt in this repo. Add any additional python dependencies that you require.

```bash
cat ~/.ansible/collections/ansible_collections/azure/azcollection/requirements-azure.txt
```

Building the EE
------------

Clone this repo, edit requirements.txt as need and run the build:

```bash
ansible-builder build -t <registry_name>/<image_name>:<image_tag>
```

For example:

```bash
ansible-builder build -t quay.io/pharriso/azure_ee:1.0
```

Pushing the EE to a container registry
------------

The image is now ready to be pushed to a container registry or automation hub:

```bash
podman login quay.io
podman push quay.io/pharriso/azure_ee:1.0
```
