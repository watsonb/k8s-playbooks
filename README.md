# playbooks

This directory contains Ansible playbooks used to deploy and configuration
manage TBD...

# Top-level playbooks

Pertinent top-level playbooks are described below

## provisionSystem.yml

This is the main provisioning playbook that includes several other playbooks to
configuration-manage various Virtual Machines (VMs).  You typically run the
playbook as follows:

    ansible-playbook -i playbooks/inventory/<file> playbooks/provisionSystem.yml --ask-vault-pass
    
Where <file> is a particular inventory file.  More on inventories in the next
section.

The --ask-vault-pass switch will cause Ansible to interactively prompt you to
supply the password to the Ansible vault.  The vault contains sensitive
information (e.g. passwords) and the playbook cannot be run without the vault.

If you've secured the password in a text file (e.g. in a place only readable by
the ansible user), then you can run the command like this (e.g. in Jenkins):

    ansible-playbook -i playbooks/inventory/<file> playbooks/provisionSystem.yml --vault-password-file /path/to/password_file.txt

# Inventories

We define several inventories for different environments/purposes.  Ben Watson
typically uses the inventories/ece and inventories/omaha files for developing
Ansible playbooks locally (in Omaha).  Other inventories exist for other
environments and define environment-specific groups within them for the sake
of variable substitution (see below).  For example, the inventories/azure_int
file is designated for the Integration environment in Microsoft's Azure GovCloud
and defines a group named integration-environment for the sake of defining
variable values specific to that environment.

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
