# Day 3: Secure Root SSH Access

**Objective**: Disable the SSH access of the root user in the servers to improve security.

**Context**: Allow to login via SHH increase the possibilities of attacks. The security team has rolled out new protocols, including the restriction of direct root SSH login.

**Steps**:

```sh
# This has to be for the 3 stapp servers,
tony@stapp01
sudo vi /etc/ssh/sshd_config # update PermitRootLogin yes to No
sudo systemctl restart sshd # restart sshd
sudo sshd -T | grep permitrootlogin # Check if the Permission is no
exit
```

**NOTE**: I forgot to exit with every user. Also I enter in `/etc/ssh/ssh_config` instead of `/etc/ssh/sshd_config` (`ssh` instead `sshd`).
