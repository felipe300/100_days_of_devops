# Day 2: Temporary User Setup with Expiry

**Objective**: Ensure smooth access management, a temporary user account with an expiry date is needed.

**Context**: Temporal access management accounts reduce security risks. Define an expiration date to avoid inactive hidden access to persists.

**Steps**:

```sh
ssh tony@stapp01 # Login to Server 1
sudo useradd -m -e 2027-03-28 ravi # add user expired ravi
sudo chage ravi -l # check expiration date
sudo userdel ravi
sudo rm -rf /home/ravi
```

**NOTES**

First I created an user as the challenge day one, but it was a mistake. I have to remove the user and delete the folder home for ravi.
