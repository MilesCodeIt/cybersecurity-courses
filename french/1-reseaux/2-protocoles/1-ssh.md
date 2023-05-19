# 1. SSH (Secure Socket Shell)

SSH est un protocole réseau qui permet aux administrateurs d'accéder à distance à un ordinateur, en toute sécurité.

## Utilisation d'`ssh`

```bash
# `ssh` vient par défaut sur les dernières versions de Windows 10 et sur Windows 11.
ssh username@xxx.xxx.xxx.xxx
```

Si c'est la première fois que vous vous connectez sur cette IP, vous risquez d'avoir un prompt dans ce genre...

```console
The authenticity of host 'ssh.example.org (xxx.xxx.xxx.xxx)' can't be established.
......... key fingerprint is ........................................
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Dans ce cas, vous pouvez tout simplement écrire `yes` pour ajouter la clé dans la liste des hôtes connus.

## Utilisation de `scp`

Vous pouvez aussi utiliser le protocole SSH pour le transfert de fichiers.

### Copie d'un fichier sur notre PC vers le serveur

```bash
scp ./monFichier.txt username@ipDuServeur:/home/username/leFichier.txt
```

Ici, on copie le fichier `monFichier.txt` de notre PC vers `/home/username/leFichier.txt` dans le serveur distant.

### Copie d'un fichier du serveur vers notre PC

C'est la même commande que précédemment, cependant on inverse l'ordre.

```bash
scp username@ipDuServeur:/home/username/leFichier.txt ./monFichier.txt
```

### Copier un dossier (`-r`)

On peut directement copier un dossier en utilisant l'argument `-r`.

```bash
scp -r ./monDossier username@ipDuServeur:/home/username/
```
