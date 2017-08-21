
# Ansible playbooks to build LocalWiki instances


## Playbooks

### Overview

* `firstboot.yml` set up *beachmaster* account for further tasks and safe guard *root*.  This is the only playbook that needs to be run with *root* remote user (or other user having root access.) You only need to run this once for each machine.  In fact, you may not be able to run this again because SSH login for *root* will be disallowed.  You may want to keep another SSH connection alive in case this blocks all your remote access to the machine.
* `os.yml` updates OS and system-level settings such as hostname, timezone.  Run this regularly to get OS updates.
* `provision.yml` set up environment for the application.  This is where division of labor starts.  You only need to run this once when the environment changes, for example a machine is added or removed.
* `deploy.yml` deploys the application.  Run this when releasing a new version.

### Usage

```
# Create Linode, add to `hosts`, and then
$ ansible-playbook -u root -k -e target=web0 playbooks/firstboot.yml  # needs root password
$ ansible-playbook -u beachmaster playbooks/os.yml
$ ansible-playbook -u beachmaster playbooks/provision.yml
$ ansible-playbook -u beachmaster playbooks/deploy.yml
```
## TODO

* [ ] Switch to geerlingguy.postgresql.
