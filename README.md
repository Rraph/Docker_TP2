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
└─vg01-data 253:2    0  15G  0 lvm  /data
```

Pour faire en sorte que le volume reste monter au redémarrage on édite le fichier /etc/fstab on rajoute la ligne 

```
/dev/vg01/data /data    ext4    defaults        0 0
```

### 3. Installation de Gitlab-ce

Une fois avoir suivi l'installation (longue..très longue..) de gitlab-ce, je créé une key ssl. Remplis les champs ne sert pas forcément à grand chose éxcepté le champ "Common Name" : on y renseigne le hostname set en début de TP. Si vous ne vous en souvenez plus :

```
    $ hostname
```

voici la config : 

```
Country Name (2 letter code) [XX]:47
State or Province Name (full name) []:France
Locality Name (eg, city) [Default City]:Agen
Organization Name (eg, company) [Default Company Ltd]:Raph
Organizational Unit Name (eg, section) []:osef
Common Name (eg, your name or your server's hostname) []:**tp2.gitlab**
Email Address []:raphael.beghin@live.fr
```
