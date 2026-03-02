# Day 32: Git Rebase

**Objective**: Ensure that code flows smoothly from a developer's workspace to the central repository without permission errors or data loss.

**Context**: One of the developers in the development application team is working on a new feature, but some changes have benn push to the main branch.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

ls /opt/[WORKING_REPO].git # working repo (apps)
ls /usr/src/kodekloudrepos/[CLONED_REPO] # cloned repo (apps)
cd /usr/src/kodekloudrepos/[CLONED_REPO]
git branch # got "master" and "feature"
git log --online # Do this for both branches
git rebase [FROM_REPO] [DESTINY_REPO]
git push origin feature # ERROR: [rejected], read the hints:

git config pull.rebase true # copy the command need it from the hints

git pull origin feature # bring changes from master branch
git push origin feature # now, OK

exit
```

**Notes**

Git rebase "hints"

```sh
git push origin feature
To /opt/apps.git
 ! [rejected]        feature -> feature (non-fast-forward)
error: failed to push some refs to '/opt/apps.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

You need to "pull" the changes from your master branch, `git pull origin feature`

```sh
git pull origin master
From /opt/apps
 * branch            master     -> FETCH_HEAD
Already up to date.
[root@ststor01 apps]# git pull origin feature
From /opt/apps
 * branch            feature    -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

Update your git rebase configuration: `git config pull.rebase true`

Git Rebase

Rebase takes your commits, lifts them up, and places them on top of the very latest commit of the target branch. It literally changes the "base" of your work.

Common Options:

- **pick**: Use the commit as it is.
- **squash**: Combine this commit with the one before it (great for fixing "typo" commits).
- **reword**: Keep the changes but change the commit message.
- **drop**: Delete the commit entirely.

```sh
# 1. Switch to your branch:
git checkout feature-login

# 2. Move your work to the top of the current main:
git rebase main

# 3. Interactive Rebase (-i)
git rebase -i HEAD~3
```

```text
pick f7f3f6d Añadir login
pick 310154e Corregir typo en login  <-- ¡Esto no debería ser un commit aparte!
pick a5f1b2c Añadir validación de password
```
