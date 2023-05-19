# 3. FTP (File Transfert Protocol)

Le protocole FTP permet, depuis un ordinateur, de copier des fichiers vers un autre ordinateur du réseau, ou encore de supprimer ou de modifier des fichiers sur cet ordinateur.
La variante de FTP protégée par les protocoles SSL ou TLS (SSL étant le prédécesseur de TLS) s'appelle FTPS.

## Utilisation

### Connexion

Sous Linux on utilise la commande `ftp`.

```console
$ ftp {adresse IP}
[...]
Name ({ip}:{domaine}): <entrez votre nom d'utilisateur>
[...]
Password: <entrez votre mot de passe>
[...]
ftp>
```

Lorsque vous voyez `ftp>`, vous êtes connecté dans la console.

### Commandes

- help or ? - Liste toutes les commandes disponible sur le ftp.
- cd - change le repertoire sur la machine distante.
- lcd - change le repertoire sur la machine locale.
- ls - Liste lee nom des fichiers et des repertoires dans repertoire distant actuel.
- mkdir - crée un nouveau répertoire sur la machine distante.
- pwd - affiche le chemin d'accès sur la machine distante.
- delete - Supprime un fichier dans le repertoire de la machine distante.
- rmdir- Supprime un repertoire dans le repertoire de la machine distante.
- get - Copie un fichier de la machine distante à la machine locale.
- put - Copie un fichier de la machine locale à la machine distante.
