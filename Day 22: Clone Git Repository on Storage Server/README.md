# Day 22: Clone Git Repository on Storage Server

**Objective**: Clone a git Repository

**Context**: The development team needs a copy of the repo on Storage Server.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su

ls /opt/[PROJECT_NAME].git # location of the project (project.git)
ls /usr/src/[DESTINY_PROJECT] # location to store the project (kodekloudrepos)
cd /usr/src/[DESTINY_PROJECT]
git clone /opt/[PROJECT_NAME].git

# you will get a message: "warning: You appear to have cloned an empty repository."
cd /[PROJECT_NAME].git
ls -la # to check the repo

exit
```

**NOTE**:

- With `git clone`, you can clone remote and local repositories.
- The repository that you are cloning, it's a "bare" repo. You are setting up a local git workflow, likely on a server or a lab environment, that hasn't had any commits yet will indeed trigger that "empty repository" warning.
