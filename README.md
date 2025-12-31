# Project PasCam 8
> Encrypt and share passwords using a Discord bot. V8. Spring 2024.

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
> **`image`** [`project-pascam:latest`](https://hub.docker.com/repository/docker/lxrbckl/project-pascam/general) <br>
> **`variable`** `purpose of variable`

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
> `variable` **`required?`** `variable purpose`

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
> `variable` **`required?`** `variable purpose`

# 

*`autosave.sh`*
```bash
#!/bin/bash


projectPath=;


sudo rm -r $projectPath/data/*
sudo cp -r $projectPath/backup/* $projectPath/data/
```
> `variable` **`required?`** `variable purpose`

---

---

<p align="center">
  
  <img width="155" src="https://i.postimg.cc/R0sSxJpD/IMG-5018.jpg">
  <img width="155" src="https://i.postimg.cc/wxtvHFpc/IMG-5019.jpg">
  <img width="155" src="https://i.postimg.cc/HxFTVDg0/IMG-5020.jpg">

</p>
<div align="center">
  
  *This project is a heartfelt tribute to our beloved bunny, Tribble. Gone but not forgotten.*

</div>
