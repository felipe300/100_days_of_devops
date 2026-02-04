# Day 8: Install Ansible

**Objective**: Install Ansible as automatization tool, and config manager.

**Context**: It has been decided to use Ansible as tool, and config manager for its simplicity and low requirements. The team have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

**Steps**:

```sh
pip3 --version # Check if pip3 is installed
sudo pip3 install ansible==4.10.0 # Install Ansible 4.10.0
ansible --version # Check Ansible version
```

**NOTE**: Very straight forward task.
