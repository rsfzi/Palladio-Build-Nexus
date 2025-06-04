# Palladio-Build-Nexus
Setup a nexus cache for palladio builds.  

## Setup
### Install
Create nexus service.

#### Linux
Clone this repo to: `<develop>/Palladio-Build-Nexus`

##### Podman
This configuration expects to folders to exist and owned by user id 200 on the host machine:
```
sudo mkdir -p /mnt/repository/nexus-data
sudo mkdir -p /mnt/backup/nexus
sudo chown 200 /mnt/repository/nexus-data
sudo chown 200 /mnt/backup/nexus
```

Create and start the nexus service.
```
cd /etc/containers/systemd
sudo ln -s <develop>/Palladio-Build-Nexus/linux/podman/nexus.container
sudo systemctl daemon-reload
sudo systemctl start nexus
```

#### Windows
##### Podman
```
podman machine init nexus
podman machine start nexus
podman machine ssh nexus
sudo yum -y install git
```
Configure git to access github from nexus machine.
Then clone this repo to: `<develop>/Palladio-Build-Nexus`
```
podman machine ssh nexus
mkdir -p <develop>
cd <develop>
git clone git@github.com:rsfzi/Palladio-Build-Nexus.git
```
Prepare folders
```
sudo mkdir -p /mnt/repository/nexus-data
sudo mkdir -p /mnt/backup/nexus
sudo chown 200 /mnt/repository/nexus-data
sudo chown 200 /mnt/backup/nexus
```
Create and start the nexus service.
```
cd /etc/containers/systemd
sudo ln -s <develop>/Palladio-Build-Nexus/linux/podman/nexus.container
sudo systemctl daemon-reload
sudo systemctl start nexus
```

Follow these instructions:
[autostart-podman-containers-on-windows](https://medium.com/@saderi/how-to-autostart-podman-containers-on-windows-9db2185351e1)

### Prepare
Setup initial nexus DB.
#### Linux
```
sudo systemctl stop nexus
cd /mnt/repository/nexus-data/db
sudo cp <develop>/Palladio-Build-Nexus/nexus/nexus.mv.db .
sudo systemctl start nexus
```

#### Windows
##### Podman
```
podman machine ssh nexus
sudo systemctl stop nexus
cd /mnt/repository/nexus-data/db
sudo cp <develop>/Palladio-Build-Nexus/nexus/nexus.mv.db .
sudo systemctl start nexus
```

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
