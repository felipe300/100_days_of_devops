# Day 4: Script Execution Permissions

**Objective**: give execution permissions to a script that all users can used

**Context**: Some files in Linux need to share between users. A file the correct permission to be executed by all users.

**Steps**:

```sh
ssh tony@stapp01 # move to the server
ls -l /tmp/xfusioncorp.sh # check permissions: show no permission at all
sudo chmod 775 /tmp/xfusioncorp.sh # give full permissions
ls -l /tmp/xfusioncorp.sh # check permissions: show full permissions
sudo -u nobody /tmp/xfusioncorp.sh # check permission as another user
```

**NOTE**: Just check the right permissions. In this exercise they ask for full permissions.
