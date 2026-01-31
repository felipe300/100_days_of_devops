# Day 7: Linux SSH Authentication

**Objective**: Config an SSH access with no password through public keys.

**Context**: Access through public keys with SSH allows to: automate remote tasks, avoid the use of password, and increase security.

**Steps**:

```sh
# By default you are in thor@jumphost user
ls ~./ssh # check for existing ssh keys, especially files 'id_rsa' & 'id_rsa.pub'
ssh-keygen -t rsa -b 2048 # Generate a pair ssh keys
# For this challenge press Enter to create files
# Then, press Enter twice to avoid to create a password
ls ~./ssh
ssh-copy-id tony@stapp01.stratos.xfusioncorp.com # Copy key into a new server
# Now try logging into the machine, with: "ssh 'tony@stapp01.stratos.xfusioncorp.com'"
ssh tony@stapp01.stratos.xfusioncorp.com hostname # check hostname
```

**NOTE**: Do the copy for each server: `tony`, `steve`, and `banner`.
