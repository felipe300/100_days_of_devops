# Day 28: Git Cherry Pick

**Objective**: Understand and select a specific commit.

**Context**: The teams working on a cloned repository in a different branches. But the team needs a commit in the other branch to keep working.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

cd /opt/[REPO].git # working repo (media) - master branch
git branch
cd /usr/src/kodekloudrepos/[WORKING_REPO] # cloned repo (media) - feature branch
git branch
git switch master
git cherry-pick [HASH] # (a1b2c3d)
git push -u origin master

exit
```

**Notes**:

Think of git **cherry-pick as a "copy-paste"** for specific commits.

Instead of merging an entire branch (which brings over every change), cherry-picking allows you to pick **one specific commit** from one branch and apply it to your current branch.

When to use it?

- **Bug Fixes**: You fixed a bug on a `development` branch but need that same fix on the `production` branch immediately without moving other unfinished features.
- **Undo/Recover**: You accidentally committed something to the wrong branch and want to move it to the right one.
- **Collaboration**: A teammate has a specific helper function in their branch that you need in yours.

```sh
git log --oneline # Find the Commit Hash (a1b2c3d)
git switch main # Switch to the Target Branch (main, master, or the one you need)
git cherry-pick [HASH] # Run the Pick (a1b2c3d)
```
