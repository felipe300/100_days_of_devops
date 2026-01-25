# Day 1: Linux User Setup with Non-Interactive Shell

**Objective**: Create a user named `john` with a non-interactive shell on `App Server 2`.

**Context**: Users shouldn't be created with a non-interactive shell.

**Steps**:

By default your user should be

```sh
# example <user>@<hostname>
# default thor@jumphost
> steve@stapp02 # change to "App server 2"

which "nologin" # find folder "nologin", because it is a non-interactive shell
sudo useradd -s /sbin/nologin john # add user john
id john # check if user was created
grep "^john" # check assigned shell
```
