# TP5 - Systèmes de fichiers, partitions et disques

## Exercice 1. Disques et partitions

1, 2, 3.

```bash
$ sudo fdisk /dev/sdb
```

4.

```bash
$ sudo mkfs -t ext4 /dev/sdb1
$ sudo mkfs -t ntfs /dev/sdb2
```

5. 

Le système de fichiers n'est pas encore monté.

6. 

```bash
$ sudo mkdir /data
$ sudo mkdir /win
$ sudo nano /etc/fstab
```

Il faut ajouter les lignes suivantes :

```bash
/dev/sdb1 /data ext4 defaults 0 2
/dev/sdb2 /win ntfs defaults 0 2
``` 

7. 

```bash
$ sudo mount -a
```

8, 9.

```bash
$ sudo apt install virtualbox-guest-additions-iso
```

Le dossier partagé créé sur virtualbox est fonctionnel.


## Exercice 2. Partitionnement LVM

1. 

```bash
$ sudo umount /data
$ sudo umount /win
$ sudo nano /etc/fstab
```

2.

```bash
$ sudo fdisk /dev/sdb
```

3.

```bash
$ sudo pvcreate /dev/sdb1
$ sudo pvdisplay
```

4. 

```bash
$ sudo vgcreate vg1 /dev/sdb1
$ sudo vgdisplay
```

5. 

```bash
$ sudo lvcreate -n lvData -l 100%FREE vg1
```

6. 

```bash
$ sudo mkfs -t ext4 /dev/vg1/lvData
$ sudo mkdir /data
$ sudo nano /etc/fstab
```

Il faut ajouter la ligne suivante :

```bash
/dev/vg1/lvData /data ext4 defaults 0 2
```

7. 

```bash
$ sudo fdisk /dev/sdc
$ sudo pvcreate /dev/sdc1
$ sudo pvdisplay
```

8. 

```bash
$ sudo vgextend vg1 /dev/sdc1
$ sudo vgdisplay
```

9. 

```bash
$ sudo lvresize -l +100%FREE /dev/vg1/lvData
$ sudo resize2fs /dev/vg1/lvData
```
