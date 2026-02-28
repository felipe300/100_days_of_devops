# Day 31: Git Stash

**Objective**:

**Context**: One of the developers from the application team stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

cd /usr/src/kodekloud/[PROJECT_NAME] # (official)
ls
git stash list # list of stash and look for the specific stash
git stash apply [STASH_ID] # restore to specific stash (stash@{1})
git status
git add .
git commit -m "XXX"
git remote
git push origin origin

exit
```

**Notes**:

Git Stash

The `git stash` lets you sweep your uncommitted changes into a temporary storage area, leaving your workspace clean so you can switch tasks.

When you run a stash command, Git takes your modified tracked files and staged changes and saves them in an internal stack. Your working directory reverts to the state of the last commit (`HEAD`).

| Command           | What it does                                             |
| ----------------- | -------------------------------------------------------- |
| `git stash`       | Saves your changes and reverts to a clean state.         |
| `git stash list`  | Shows all your saved "scraps" of work.                   |
| `git stash apply` | Brings the changes back but keeps a copy in the stash.   |
| `git stash pop`   | Brings the changes back and deletes them from the stash. |
| `git stash drop`  | Deletes a specific stash without applying it.            |

```sh
# You're in the middle of login logic
git stash

# Your workspace is now clean. Switch and fix the bug.
git checkout main
# ... fix bug, commit, and push ...

# Back to work!
git checkout feature-login
git stash pop
```
