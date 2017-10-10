# k8s-playbooks

This directory contains Ansible playbooks used to deploy and configuration
manage a Kubernetes cluster with etcd.  The basis of this work is a GitHub
gist here: https://github.com/kelseyhightower/kubernetes-the-hard-way

TODO: This will require some refactoring for ease of maintenance.  That is,
this playbook is almost entirely tasks in a series of plays vice an extensive
use of generic roles.  You have been warned!

# Prerequisites (for your Ansible controller)

## certifi python package
For some reason, the current version of certifi doesn't jive with Google Cloud
Platform.  You need a specific version, like so:

pip uninstall -y certifi && pip install certifi==2015.04.28

## apache-libcloud
You need apache-libcloud for Ansible GCP support:

pip install apache-libcloud

## Ansible controller on GCP with gcloud
This was all run from a Linux VM running on the Google Cloud Platform (GCP).
The VM has Ansible v2.3 installed (as a Python virtual environment) and also
has the Google Cloud SDK installed (providing the gcloud command-line tools).

# Top-level playbooks

Pertinent top-level playbooks are described below

## kubernetesTheEasyWay.yml
This playbook is a play on words as it is named after a GitHub gist entitled
"Kubernetes the Hard Way", which was the inspiration of this playbook.  Running
this playbooks includes several additional top-level playbooks which provision
GCP computes/network resources and install/configuration-manage software onto
those resources, thus yielding a fully functional Kubernetes cluster.

## deleteGcPEnvironment.yml

This playbook cleans up the GCP environment/account by deleting all VMs and
network resources that were created via the kubernetesTheEasyWay playbook.

# Inventories

gcp_dev is the only inventory at the moment and defines 3 Kubernetes controllers
and 3 workers per the "Kubernetes the Hard Way" tutorial.

# Variables

TBD

# Roles

The table below describes some of the roles:

|role|description|
|---|---|
|role_template|This is a "blank" role that is used as a template/basis for creating new roles|

# License

TBD

# Author Information

|Author|E-Mail|
|---|---|
|Ben Watson|bwatson@mitre.org|
