# Linux

## Users and Groups
```
id NAME
adduser [user]
deluser [username]
addgroup [user] [group]
delgroup [user] [group]
passwd [user]
```

## Compression with tar
```
tar [options] [path]

  OPTIONS
    -x  Extract
    -c  Compress
    -f  Use a file
    -z  Filter with gzip
    -j  Filter with bzip2
```

## Disk and Partitions
```
df -h   Show mount points
fdisk -l  Show partitions

dd if=/entrypoint of=/outpoint bs=512 count=1

update-grub2
```

### LVM
```
pvcreate /dev/sdx
pvs   List physical volumes in LVM
pvremvoe /dev/sdx

vgcreate group_name device
vgextend group_name device
vgreduce group_name device
vgs | List groups

lvcreate [options] group_name
  -n name
  -L {size}G
lvextend -L+10G /logical_volume
lvs
```

## Systemd
```
systemctl daemon-reload
systemctl status SERVICE
systemctl is-active SERVICE
systemctl start SERVICE
systemctl stop SERVICE
systemctl enable SERVICE
systemctl disable SERVICE
systemctl cat SERVICE

```

## Network
```
nc Open TCP/UDP listen ports
netstat -an   check ports listening
ifconfig
ifdown [interface]
```

## Search
```
find [directory]
locate [directory]
whereis [command]
```

## Pipes & Redirects
