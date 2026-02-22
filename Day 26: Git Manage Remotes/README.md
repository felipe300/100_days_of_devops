# Day 26: Git Manage Remotes

**Objective**: Create a new remote branch and manage it.

**Context**: The xFusionCorp development team added updates to the project that is maintained. Recently some changes were made on Git server. The DevOps team added some new Git remotes, so we need to update remote.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

ls /opt/[PROJECT_NAME].git # check project (official)
ls /usr/src/kodekloudrepos/[PROJECT_NAME] # cloned  project
ls /opt/[NEW_REMOTE_PROJECT].git # check project to point new remote branch (xfusioncorp_official)
cat /tmp/index.html # check file

cd /usr/src/kodekloudrepos/[PROJECT_NAME]
git remote -v # check fetch and pull directories
git remote add [NEW_REMOTE_NAME] /opt/[NEW_REMOTE_PROJECT].git # add remote branch (dev_official) to the project (xfusioncorp_official)
git remote -v
cp /tmp/index.html . # this should be inside your [PROJECT_NAME] (official)
git add .
git commit -m "xxx"
git push -u dev_official master # push remote

exit
```

**NOTE**:

In this task, we performed Git Remote Management. A "remote" in Git is essentially an alias or shorthand name that points to a specific URL or file path on a server where a copy of the project is hosted.

- **Repository Migration (git remote add)**: The DevOps team set up a new repository location at `/opt/xfusioncorp_official.git`. To push our local work to this specific destination, we must "register" it in our local Git configuration. By using the name `dev_official`, we created a direct bridge to this new server environment.

- **Upstream Synchronization**: By executing `git push -u dev_official master`, we aren't just uploading files; we are linking the local workflow. The `-u` (upstream) flag tracks the local master branch against the new `dev_official` remote, ensuring that future git push or git pull commands know exactly where to go.

Why the change of remote?

This process is standard when a project scales or changes infrastructure. Instead of continuing work on the legacy "official" repository, the workflow is redirected to `xfusioncorp_official` to align with the new standards and access controls defined by the `xFusionCorp` development team.
