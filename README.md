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

# Prerequisites (for Google Cloud)

## gcloud

As mentioned above, it is assumed that you have a VM running on GCP and you
have installed Ansible >= 2.3 on that box.  You have also installed the gcloud
SDK on the same box and you can run gcloud commands (e.g. to list currently
running VMs) on your GCP account.

## Ansible Configuration

Study the Google modules listed under the Cloud section of the Ansible docs.
Also have a look at the setup required for authentication with Google Cloud and
Ansible here: http://docs.ansible.com/ansible/latest/guide_gce.html.
Specifically review the section "Calling Modules By Passing Credentials" and
be prepared to create a new vars/vault.yml file with capable of setting the
variables defined in group_vars:

    gcp_service_account_email: "{{ vault_gcp_service_account_email }}"
    gcp_credentials_file: "{{ vault_gcp_credentials_file }}"
    gcp_project_id: "{{ vault_gcp_project_id }}"
    
That is to say, your vault should define the variables vault_* referenced above
and set the values of those variables to values specific to your GCP account
information.

# Top-level playbooks

Pertinent top-level playbooks are described below

## kubernetesTheEasyWay.yml
This playbook is a play on words as it is named after a GitHub gist entitled
"Kubernetes the Hard Way", which was the inspiration of this playbook.  Running
this playbooks includes several additional top-level playbooks which provision
GCP computes/network resources and install/configuration-manage software onto
those resources, thus yielding a fully functional Kubernetes cluster.

Run this playbook as follows:

    ansible-playbook -i inventories/gcp_dev kubernetesTheEasyWay.yml --ask-vault-pass

## deleteGcPEnvironment.yml

This playbook cleans up the GCP environment/account by deleting all VMs and
network resources that were created via the kubernetesTheEasyWay playbook.

Run this playbook as follows:

    ansible-playbook -i inventories/gcp_dev deleteGcPEnvironment.yml --ask-vault-pass

# Inventories

gcp_dev is the only inventory at the moment and defines 3 Kubernetes controllers
and 3 workers per the "Kubernetes the Hard Way" tutorial.  The inventory also
contains an entry for the Ansible controller itself, in this case named:

    ansible-centos7
    
Since this machine was created manually via the GCP console/portal, the
/etc/hosts file on the machine already had an entry for itself via GCP magic.
If you name your Ansible controller something else when creating it on GCP,
ensure you update the name in the inventory.

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
