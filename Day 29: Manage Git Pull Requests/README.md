# Day 29: Manage Git Pull Requests

**Objective**: Use git pull requests to avoid pushing unwanted commits

**Context**: A new user wants to push directly to master branch. To avoid this, this new user commits needs to be reviewed and approved.

**Steps**:

```sh
ssh [user]@[hostname] #  ssh max@ststor01 - Max_pass123
sudo su -

cd /story-blog
git brnach # you will get "master" and "story/fox-and-grapes"
git remote
git log
git status

git checkout master

# Click the "Gitea button" to create a pull request

exit
```

- `Gitea`

UI login info:

- Username: `max`
- Password: `Max_pass123`
  PR title : `Added fox-and-grapes story`
  PR pull from branch: `story/fox-and-grapes` (source)
  PR merge into branch: `master` (destination)

Select `tom` as "Reviewer"

- Username: `tom`
- Password: `Tom_pass123`
  PR title : Added fox-and-grapes story

Finally Review and Merge

**Notes**:

**Gitea** is a lightweight, self-hosted Git service. Think of it as a "DIY" version of GitHub. It’s written in Go, which makes it incredibly fast and capable of running on low-power hardware like a Raspberry Pi or an old laptop.

Advantages:

- **Privacy-conscious developers**: People who want to host their code on their own servers rather than a big tech company's cloud.
- **Small to medium businesses**: Companies that need an internal version control system without the high licensing costs of GitHub Enterprise or GitLab.
- **DevOps Enthusiasts**: It's a staple in "home lab" setups because it's so easy to install and uses very little RAM.

When to use it:

- **DevOps & SysAdmin Roles**: If a company manages its own infrastructure, they might ask for experience with Gitea or similar self-hosted Git solutions.
- **Niche Tech Firms**: Small agencies or specialized security firms often prefer Gitea for its simplicity and "no-nonsense" approach.
- **The "Transferable Skill" Factor**: Even if a job doesn't mention Gitea by name, listing it on your resume shows you understand the hosting and administration side of Git, not just how to "push" and "pull" code.
