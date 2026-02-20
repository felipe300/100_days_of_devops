# Day 25: Git Merge Branches

**Objective**: Use git merge to add new features

**Context**: Merge two branches with the new changes

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su -

cd /usr/src/kodekloudrepos/[REPO]/ # (cluster)
git branch
git checkout -b [NEW_BRANCH] # (datacenter)
cp /tmp/index.html .
git add .
git commit -m
git switch master
git merge [NEW_BRANCH]
git push

exit
```

**NOTE**:
