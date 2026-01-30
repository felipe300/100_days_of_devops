# Day 6: Create a Cron Job

**Objective**: Config a cron job, to automate the execution of a Linux command.

**Context**: Cron jobs allows to execute commands in Linux in a specific period of time without human intervention.

**Steps**:

```sh
ssh [user]@[hostname] # log
sudo yun install -y cronie # install cronie for cron jobs
sudo systemctl start crond # start service crond
sudo systemctl enable crond # enable service crond
sudo systemctl enable status # check service crond status
sudo crontab -e # edit cron job

*/5 * * * * echo hello > /tmp/cron_text # edit
sudo crontab -l # check if working
# manual test: wait 5 minutes
cat /tmp/cron_text
exit
```

**NOTE**: Do this steps for each server.
