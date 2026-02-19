# Day 24: Git Create Branches

**Objective**: Create a new branch to implement new features on Storage server

**Context**: Recently, the team decided to implement some new features in the application, and they want to maintain those new changes in a separate branch.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

ls -la /usr/src/kodekloudrepos/games/ # Check repository
cd /usr/src/kodekloudrepos/games/

git status
git branch # list branches
git checkout master # move to "master" branch
git checkout -b [NEW_BRANCH] # create and move to new branch (xfusioncorp_games)

exit
```

**NOTE**:

- I got some "permissions" problems to use git command in Storage server, you need to enter as a "super user" (`sudo su -`) to use git commands
