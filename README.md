# Project PasCam 8
> Encrypt and share passwords using a Discord bot. Spring 2024.
>
> **`JavaScript`** **`Docker`** `discordjs` `crypto` `git-hooks` `github-actions`

---

## Installation

*`boot.sh`*
```sh
#!/bin/bash


externalDataMount="/dev/sda1";
externalBackupMount="/dev/sdc1";

projectPath="/home/highlander/PasCam";


# check if external data #
if [ -n "$externalDataMount" ]; then

  sudo mount $externalDataMount $projectPath/data;

fi


# check if external backup #
if [ -n "$externalBackupMount" ]; then

  sudo mount $externalBackupMount $projectPath/backup;

fi


if [ ! -d "$projectPath/data" ]; then

  sudo mkdir $projectPath/data;

fi


if [ ! -d "$projectPath/backup" ]; then

  sudo mkdir $projectPath/backup;

fi


sudo docker-compose -f $projectPath/docker-compose.yaml pull;
sudo docker-compose -f $projectPath/docker-compose.yaml up;
```

# 

*`docker-compose.yml`*
```yml
version: '3.8'

services:
  pascam:
    image: lxrbckl/project-pascam:latest
    environment:
      - discordToken=

      - guildId=
      - channelId=
      - applicationId=

      - maxMembers=15
      - dataFilePath=/data/

    volumes:
      - /path/on/host:/app/data
```
> **`project-pascam:latest`** [`project-pascam:latest`](https://hub.docker.com/repository/docker/lxrbckl/project-pascam/general) <br>

# 

*`autosave.sh`*
```bash
#!/bin/bash


sleepAmount=2;

externalDataMount=;
externalBackupMount=;

projectPath=;


# check if external data #
if [ -n "$externalDataMount" ]; then

  sudo umount $projectPath/data;
  sleep $sleepAmount;
  sudo mount $externalDataMount $projectPath/data;

fi


# check if external backup #
if [ -n "$externalBackupMount" ]; then

  sudo umount $projectPath/backup;
  sleep $sleepAmount;
  sudo mount $externalBackupMount $projectPath/backup;

fi
```

# 

*`backup.sh`*
```sh
#!/bin/bash


sleepAmount=2;
externalBackupMount=;
projectPath=;


if [ -n "$externalBackupMount" ]; then

  sudo cp -r $projectPath/data/* $projectPath/backup;

  sudo umount $projectPath/backup;
  sleep $sleepAmount;
  sudo mount $externalBackupMount $projectPath/backup;

fi
```

# 

*`autosave.sh`*
```bash
#!/bin/bash


projectPath=;


sudo rm -r $projectPath/data/*
sudo cp -r $projectPath/backup/* $projectPath/data/
```

---

<p align="center">
  
  <img width="155" src="https://immich.lxrbckl.com/api/assets/bd46a542-6fe3-4d32-89aa-73b0b00eee93/thumbnail?slug=dedications&size=preview&c=oKcJDQJ%2FiI95d1eHiHZYp5RfA5go&edited=true">

</p>
<div align="center">
  
  *This project is a heartfelt tribute to our beloved bunny, Tribble. Gone but not forgotten.*

</div>
