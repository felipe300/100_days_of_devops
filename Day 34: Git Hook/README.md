# Day 34: Git Hook

**Objective**: Learn about Git Hooks.

**Context**: The team want to setup a hook on this repository.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh natasha@ststor01
sudo su

ls /opt/[MAIN_REPO].git/ # base project (games)
cd /usr/src/kodekloudrepos/[CLONED_REPO]/ # cloned repo (games)

cd .git/hooks/ # enter "hooks" folder
git branch # check branches
git checkout master # change to master branch
git merge [BRANCH]

# important the "hook" should be created in the "bare repo" (MAIN_REPO)
vi /opt/[MAIN_REPO].git/hooks/post-update
chmod +x /opt/[MAIN_REPO].git/hooks/post-update

git push # asked in the exercise before tag
git tag # check tags
git log --oneline # check tag added
bash /opt/[MAIN_REPO].git/hooks/post-update # Test "git tag", you will get an error. If you get an error is OK, it worked!

exit
```

- `/opt/[MAIN_REPO].git/hooks/post-update`

```bash
#! /usr/bin/env bash

# Get the current branch name
BRANCH=$(git rev-parse --abbrev-ref HEAD)

if [ "$BRANCH" == "master" ]; then
    CURRENT_DATE=$(date +%Y-%m-%d)
    TAG_NAME="release-$CURRENT_DATE"

    git tag "$TAG_NAME"
fi
```

**Notes**

Git Hooks

They are scripts that Git executes automatically every time a specific action occurs—like committing code, pushing to a server, or merging branches. They are essentially a way to automate quality control. If a hook script finishes with a non-zero status (an error), Git will abort the action you were trying to perform.

- Local vs. Server-side: Most hooks are local (running on your machine), but some run on the server (like GitHub or GitLab) to reject code that doesn't meet certain standards.

- The `.git/hooks` folder: Every Git repository has a hidden folder where these scripts live. By default, Git populates it with `.sample` files.

The Scenario: You want to make sure no one accidentally commits code that has "TODO" notes left in it, or you want to ensure the code is formatted correctly.

```bash
#!/bin/sh

# Check if the word "TODO" exists in the files being committed
if grep -q "TODO" $(git diff --cached --name-only); then
    echo "ERROR: You have 'TODO' labels in your code. Fix them before committing!"
    exit 1
fi
```

1. You finish a feature but leave a comment: `// TODO: fix this later`.
2. You run `git commit -m "Finished feature"`.
3. The hook runs, finds the "TODO", and blocks the commit.
4. You are forced to clean up your code before you can successfully save your work.
