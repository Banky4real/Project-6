## **Documentation for Project 6**

### Entire View of the newly created Block Devices 
`lsblk`
![list-of-newly-created-Block-devices](./Images-WebServer/newly-created-block-device-list.png)

### Partioning Block Devices
`sudo gdisk /dev/xvdf`
![First-Block-Partitioning](./Images-WebServer/first-volume-partition.png)

### Entire View of all Partitioned Block
`lsblk`
![Entire-view-of-all-partitioned-Blocks](./Images-WebServer/all-volumes-partitioned.png)

### LVM2 Installation
`sudo yum install lvm2`
![Installing-LVM2](./Images-WebServer/LVM2-installation.png)

### LVM2 Installed
`which lvm`
![Installed-LVM2](./Images-WebServer/LVM2-Installed.png)

### Marking the Partitions as Physical Volumes
`sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`
![Marking-partitions-as-physical-volumes](./Images-WebServer/marking-our-partions-as-physical-volumes.png)

### Physical-volumes-created
`sudo pvs`
![Partitions-active-as-physical-volumes](./Images-WebServer/our-partitions-active-as-physical-volumes.png)

### Creating-Volume-Group
`sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1`
![Creating-Volume-Group](./Images-WebServer/Creating-volume-groups.png)

### Volume-Group-Successfully-Created
`sudo vgs`
![Volume-Group-Created](./Images-WebServer/volumegroup-successfully-created.png)

### Creating-Logical-Volumes
`sudo lvcreate -n apps-lv -L 14G webdata-vg`
`sudo lvcreate -n logs-lv -L 14G webdata-vg`
`sudo lvs`
![Logical-Volumes-Created](./Images-WebServer/Logical-Volumes-created.png)

### Formatting-Logical-Volumes-with-EXT4-Filesystem
`sudo mkfs -t ext4 /dev/webdata-vg/app-lv`
`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`
![Formatting-Logical-Volumes](./Images-WebServer/formating-logical-volumes-with-ext4-file-system.png)

### Creating-Directory-to-Store-website-files
`sudo mkdir -p /var/www/html`
![Directory-for-website-files](./Images-WebServer/creating-directory-to-store-website-files.png)

### Creating-Directory-to-Store-Log-Files
`sudo mkdir -p /home/recovery/logs`
![Directory-for-Log-files](./Images-WebServer/creating-directory-to-store-log-files.png)

### Mounting-Website-files-directory-on-app-lv
`sudo mount /dev/webdata-vg/apps-lv /var/www/html`
![Mounting-Directory-on-app-lv](./Images-WebServer/app-lv-mounted-on-directory-html-created.png)

### Mounting-Log-files-directory-on-logs-lv
`sudo mount /dev/webdata-vg/logs-lv /var/log`
![Mounting-Log-Directory-on-logs-lv](./Images-WebServer/log-files-mounted-on-logs-lv.png)

### Updating-fstab
`sudo vi /etc/fstab`
![fstab-updated](./Images-WebServer/fstab-updated.png)

### Entire-setup-of-Volumes
`df -h`
![View-of-the-entire-setup-of-volumes](./Images-WebServer/entire-setup-view-of-volumes.png)

## **Preparing Database Server**

### Volumes-Attached-for-DB-Server
`lsblk`
![volumes-attached](./Images-DBServer/Volumes-attached-for-DBServer.png)


### Volumes-successfully-partitioned
`sudo gdisk /dev/xvdf`
![volumes-successfully-partitioned](./Images-DBServer/Successful-partitioning-of-volumes.png)

### Volumes-marked-as-physical-volumes
`sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`
![Physical-volumes-created](./Images-DBServer/Volumes-marked-as-physical-volumes.png)

### Installing LVM2 for DB Server
`sudo yum install lvm2`
![LVM2-Installed](./Images-DBServer/lvm2-installed-for-dbSever.png)

### Creating Volume Groups for DBServer
`sudo vgcreate vg-dbdatabase /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`
`sudo vgs`
![Volume-Group-Created](./Images-DBServer/volumes-successfully-attached-to-a-volume-group.png)

### Creating Logical Volumes
`sudo lvcreate -n db-lv -l 20G vg-dbdatabase`
`sudo vgs`
`sudo lvs`
![Logical-Volumes-Created](./Images-DBServer/logical-volume-created-for-dbServer.png)

### Formatting-Logical-Volumes-with-EXT4-Filesystem
`sudo mkfs -t ext4 /dev/vg-dbdatabase/db-lv`
![Logical-volume-formatted](./Images-DBServer/formatting-logical-volume-with-ext4.png)

### Logical Volume Mounted on DB Directory
`sudo mount /dev/vg-dbdatabase/db-lv /db`
![Logical-volume-Mounted](./Images-DBServer/logical-volume-mounted-on-db-directory.png)

### Updating fstab for DB
`sudo vi /etc/fstab`
![fstab-Updated-for-DB](./Images-DBServer/fstab-updated.png)
### mysql installation on DBServer
`sudo yum update`
`sudo yum install mysql-server`
![my-sql-server-installed](./Images-DBServer/my-sql-server-installed-on-dbserver.png)