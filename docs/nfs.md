# NFS

## [Server](https://ubuntu.com/server/docs/service-nfs)

```shell
sudo apt install nfs-kernel-server
sudo systemctl start nfs-kernel-server.service
```

```shell
# /etc/exports
/srv     *(rw,sync,subtree_check)
```

```shell
sudo exportfs -a
```

## Client

```shell
mkdir ~/nas
sudo apt install nfs-common
```

```shell
# /etc/fstab
UUID=1FDD-27B1  /boot   vfat    defaults        0       0
UUID=b264f4c6-8797-4ed5-99db-e85ceebc1db4  /   ext4    defaults        0       0
192.168.1.192:/home/pi/nas /home/pi/nas nfs rw,async,hard,intr 0 0
```

```shell
echo "192.168.1.192:/home/pi/nas ${HOME}/nas nfs rw,async,hard,intr 0 0" | sudo tee -a /etc/fstab
sudo mount -a
```

## References

- [How To Partition and Format Storage Devices in Linux][1]

[1]: https://www.digitalocean.com/community/tutorials/how-to-partition-and-format-storage-devices-in-linux
