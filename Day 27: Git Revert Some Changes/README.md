# Day 27: Git Revert Some Changes

**Objective**: Revert a commit with errors

**Context**: The team have reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

cd /usr/src/kodekloudrepos/[REPOSOTPRY]/ # (apps)
git log --oneline
git revert HEAD # move to the last commit asked (HEAD), leave the editor with no changes
git status
git add . # in this case add the file "reverted"
git commit -m "[MESSAGE]" # add a message with lowercase (revert apps)
git push # publish your local commits

exit
```

**NOTE**:

- Use `git status` to track your commits changes
- Git `revert` creates a new commit that undoes the changes from a specific previous commit (in this case `HEAD`). Unlike `reset`, it doesn't delete history, making it safe for shared branches.
- As a value to `revert`, you can pass
  - `HEAD`, actual commit
  - `HEAD~n`, commit in the nth position
  - `HEAD^`, "father commit" of your actual
  - `Hash`, hash (SHA-1) id
  - branch name
  - tags
  - From a range of commits. If you want to undo the commits from `B`, `C`, and `D`. You can use `..`

```sh
git revert HEAD # HEAD
git revert 8a2b3c4 # Hash
git revert experiment # branch name
git revert v1.0.1 # tag
git revert A..D # From a range. Undo B, D, and D
```
