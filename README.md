# Docker_TP2

# TP Réalisé par Raphaël BEGHIN

## Part.1 Gitlab
### 1. Ajout d'un disque

Pré-requis : Tout d'abord j'ai ajouté un disque "physique" à ma VM sur virtualbox.

Par la suite, il faut allouer 15Gb de ce disque pour la partition data grâce au LVM.

```
    $ pvcreate /dev/sdb
    $ vgcreate vg01 /dev/sdb
    $ lvcreate -L 15G -n data vg01
    $ mkfs.ext4 /dev/vg01/data
    $ mkdir /data
    $ mount /dev/vg01/data /data
```

On vérfie que tout s'est bien passé 

```
    $ lsblk /dev/sdb 
    
    NAME        MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sdb           8:16   0  30G  0 disk
+-vg01-data 253:2    0  15G  0 lvm  /data
```

Pour faire en sorte que le volume reste monter au redémarrage on édite le fichier /etc/fstab on rajoute la ligne 

```
/dev/vg01/data /data    ext4    defaults        0 0
```
