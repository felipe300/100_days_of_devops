# Day 5: SElinux Installation and Configuration

**Objective**: Install SELinux and disable it permanently.

**Context**: SELinux (Security-Enhanced Linux) add a layer of security through control access policies. Some laboratories or environment needs SELinux to be dibbled to work correctly, or to avoid to be block.

**Steps**:

```sh
ssh <user>@<hostname>
cat /etc/os-release # check ID="centos" and ID_LIKE="rhel fedora"
sudo yum install -y selinux-policy selinux-policy-targeted # Install SELinux
sudo vi /etc/selinux/config
 # look for "SELINUX=" and change the value to disabled
 # look for "SELINUXTYPE=" and change the value to targeted
exit
sudo reboot # just if asked
```

**NOTE**: I got `connection refuse por 22`, several times,even thou the server and the host name where correct. I had to restart the lab.
