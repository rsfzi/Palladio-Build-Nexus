# Palladio-Build-Nexus
Setup a nexus cache for palladio builds.  
Clone this repo to: `<develop>/Palladio-Build-Nexus`

## Setup
### Install
#### Linux
##### Podman
Create link to: 
```
cd /etc/containers/systemd
ln -s <develop>/Palladio-Build-Nexus/linux/podman/nexus.container
systemctl daemon-reload
systemctl start nexus
```

### Prepare
#### Setup initial DB
##### Linux
```
systemctl stop nexus
cd /mnt/repository/nexus-data
cp <develop>/Palladio-Build-Nexus/nexus/nexus.mv.db .
systemctl start nexus
```

### Initialize / repair blob store
1. Open the local [nexus instance](http://localhost:8081).
1. Login with: admin / nexus.
1. Go to _Settings/System/Tasks_.
1. Run task: _backup_repair_blob_store_

## Maven
Use the _maven/settings.xml_ as user settings file.

### Linux
Create link: 
```
mkdir -p .m2
cd .m2
ln -s <develop>/Palladio-Build-Nexus/maven/settings.xml
```
