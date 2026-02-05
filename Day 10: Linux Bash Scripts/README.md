# Day 10: Linux Bash Scripts

**Objective**: Automate the backup of a static website.

**Context**: Automate the backup of a static website in App Server X to backup server.

**Steps**:

```sh
ssh [user]@[hostname]
zip --version # check zip if exits
sudo yum install -y zip # install zip
sudo mkdir -p /scripts /backup # create "scripts" and "backup" folder
sudo chown [user]:[user] /scripts /backup

ssh-keygen -t rsa # generate key
ssh-copy-id clint@stbkp01 # copy key into Back up server
vi /scripts/[FILE_NAME].sh # edit file
chmod +x /scripts/[FILE_NAME].sh
/scripts/[FILE_NAME].sh
exit
```

- `/script/xyz.sh`

```bash
#!/bin/bash

BACKUP_DIR="/backup"
SOURCE_DIR="/var/www/html/[FOLDER_NAME]"
BACKUP_FILE="xfusioncorp_news.zip"

zip -r "${BACKUP_DIR}/${BACKUP_FILE}" "${SOURCE_DIR}"
zip -r /backup/xfusioncorp_beta.zip /var/www/html/beta

scp "${BACKUP_DIR}/${BACKUP_FILE}" clint@stbkp01:/backup/
```

**NOTE**: Really important: check the name of the files (`FILE_NAME`) and the folder (`FOLDER_NAME`), and from what server (`SERVER_APP`) are you moving for backup server.
