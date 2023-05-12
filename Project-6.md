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