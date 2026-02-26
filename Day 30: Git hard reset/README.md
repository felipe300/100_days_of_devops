# Day 30: Git hard reset

**Objective**: Clean the working commit tree

**Context**: The application development team was working on a git repository. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the `HEAD`.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh max@ststor01 - Max_pass123
sudo su -

cd /usr/src/kodeklourepos/[PROJECT_NAME]/
ls
git status # clean working tree
git branch # only master
git log --oneline # check and copy the commit Hash, you want to move
git reset --hard [COMMIT_HASH]
git push origin master --force # Make changes permanently

exit
```

**Notes**:

In the `git log --oneline` you will also get the local copy (HEAD -> master) and your remote copy there (origin/master)

Think of git reset as a time machine. It moves your current branch (the `HEAD` pointer) back to a specific point in history.

1. Soft Reset (`--soft`) = "I want to delete the commit, but keep my code changes."
2. Mixed Reset (`Default`) = "I want to undo the commit and unstage my files."
3. Hard Reset (`--hard`) = "I want to wipe everything and go back to exactly how it was."

| Mode      | Moves HEAD? | Keeps Changes in Files? | "Keeps Changes in ""Stage""?" |
| --------- | ----------- | ----------------------- | ----------------------------- |
| `--soft`  | Yes         | Yes                     | Yes                           |
| `--mixed` | Yes         | Yes                     | No                            |
| `--hard`  | Yes         | No                      | No                            |

Do not forget to push your changes and force them to make the changes permanently.
