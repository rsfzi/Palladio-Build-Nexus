# Palladio-Build-Nexus
Setup a nexus cache for palladio builds.  

## Setup
Clone this repo to: `<develop>/Palladio-Build-Nexus`

### Install
Create nexus service.

#### Linux
##### Podman
```
cd /etc/containers/systemd
ln -s <develop>/Palladio-Build-Nexus/linux/podman/nexus.container
systemctl daemon-reload
systemctl start nexus
```

#### Windows
##### Podman
Follow these instructions:
[autostart-podman-containers-on-windows](https://medium.com/@saderi/how-to-autostart-podman-containers-on-windows-9db2185351e1)

### Prepare
Setup initial nexus DB.
#### Linux
```
systemctl stop nexus
cd /mnt/repository/nexus-data
cp <develop>/Palladio-Build-Nexus/nexus/nexus.mv.db .
systemctl start nexus
```

#### Windows

### Initialize / repair nexus blob store
1. Open the [local nexus instance](http://localhost:8081).
1. Login with: admin / nexus.
1. Go to _Settings/System/Tasks_.
1. Run task: _backup_repair_blob_store_

## Maven
Use the _maven/settings.xml_ as user settings file.

### Linux
Create link to user settings file:
```
mkdir -p .m2
cd .m2
ln -s <develop>/Palladio-Build-Nexus/maven/settings.xml
```
