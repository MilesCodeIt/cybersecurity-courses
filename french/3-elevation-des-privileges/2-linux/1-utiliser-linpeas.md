# Utiliser Linpeas

Linpeas est un utilitaire nous permettant de trouver plusieurs faille sur un systeme linux nous permettant d'élever nos privilèges.

## Utilisation

``` bash
wget https://github.com/carlospolop/PEASS-ng/releases/download/20230521-bc39a477/linpeas.sh -O linpeas.sh
```

Nous pouvons maintenant lancer `linpeas.sh`

## Analyse détaillé

### Informations sur le système

- tous les détails utiles sur le système d'exploitation et sa distribution, les versions et les mises à jour
- la version sudo
- si le système fonctionne à partir d'une VM (et de quel système il s'agit)

#### Alternatives

```console
$ lsb_release -a 
$ hostnamectl # includes virtualization info

$ sudo --version
```

### Logiciels disponibles

- liste des logiciels accessibles choisis dans la liste prédéfinie :

```bash
nmap aws nc ncat netcat nc.traditional wget curl ping gcc g++ make gdb base64 socat python python2 python3 python2.7 python2.6 python3.6 python3.7 perl php ruby xterm doas sudo fetch ctr
```

#### Alternatives

Vérification visuelle à partir de ces répertoires

```console
$ ls /usr/bin
$ ls /usr/sbin
```

### Processus, Cron, Services, Timers & Sockets

- liste des processus en cours d'exécution, très utile pour vérifier l'élévation des privilèges à partir d'un logiciel vulnérable exécuté en tant que super-utilisateur.

#### Alternatives

```bash
ps -U root -u root u # tous les processus exécutés en tant que root (ID réel et effectif)
```
### Informations sur le réseau


- Entrées du fichier /etc/hosts, utiles pour voir d'autres domaines ou applications
- interfaces connectées
- ports ouverts,  il est toujours bon de vérifier si quelque chose n'est pas apparu de façon cachée pendant la phase de reconnaissance.

#### Alternatives

```console
$ cat /etc/hosts
$ ip addr
sudo netstat -tulpn | grep LISTEN
```

### Informations sur l'utilisateur


- informations de base sur l'utilisateur actuel, les groupes auxquels il appartient et son statut de sudoer
- données du presse-papier si xsel et xclip sont disponibles
- utilisateurs avec console


(linPEAS rappelle spécifiquement qu'il faut vérifier les autres comptes shell pour l'escalade horizontale (ou même verticale) des privilèges.)

#### Alternatives

```console
$ id
$ sudo -l # commande très, très utile pour une escalade rapide des privilèges
$ su {utilisateur}
$ cat /etc/passwd
```

### Informations sur le logiciel


- utile pour rechercher des logiciels vulnérables

#### Alternatives

Je ne connais aucune commande, donc votre approche dépend de votre expérience et de vos connaissances - ce qu'il faut chercher et quelles applications valent la peine d'être fouillées.

### Fichiers intéressants


- liste quelques vecteurs d'attaque populaires - si quelque chose est en rouge, cela ne signifie pas qu'il est vulnérable, mais seulement qu'il peut l'être
- montre quelques noms d'utilisateur, mots de passe ou hachages possibles dans divers fichiers.

#### Alternatives

Pas beaucoup, juste une pure expérience et connaissance. Vérifier les permissions de lecture dans /etc/shadow et /root/, les hachages dans /etc/passwd ou si ce fichier est accessible en écriture.

