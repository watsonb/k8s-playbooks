# k8s-playbooks

This directory contains Ansible playbooks used to deploy and configuration
manage Kubernetes.

TODO: This will require some refactoring for ease of maintenance.

# Top-level playbooks

Pertinent top-level playbooks are described below

## provisionGcPEnvironment.yml

This playbook ensures Virtual Machines are up and running on Google Cloud
Platform.  Currently this is tied to Ben Watson's personal GCP (free trial)
account.  Update environment-level group_vars and files to "point" to other
GCP accounts if necessary.

# Inventories

We define several inventories for different environments/purposes.  The
development environment is currently defined as Ben Watson's personal GCP
account which runs several VMs to run a Kubernetes cluster.  Other environments
can be defined in other inventories.

# Variables

We make use of group_vars to define (override) various variable values based
upon group affiliation.  Typically we group entire systems into environments
(e.g., development, integration, test, staging, production, etc.).  This way, we
can alter the value of variables based on the particular environment being
managed by Ansible.  For example, development and integration environments may
pull from the 'develop' branch of Git repositories whereas staging and 
production environments may pull from the 'master' branch of these same Git
repositories.

Most roles have been developed to be completely self-contained and their 
dependency on other roles have been annotated inside their respective 
meta/main.yml files.  Moreover, most roles have sensible/sane default values
specified, though those defaults are typically geared toward development or
integration environments and should be adjusted accordingly (e.g. group_vars, 
command-line, etc.) when used to build other environments.

Navigate to a specific role's folder and view the README.md for more details.

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
