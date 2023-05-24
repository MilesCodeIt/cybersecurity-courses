# 1. Architecture de Linux

Linux est un noyau de système d'exploitation open-source développé à l'origine par Linus Torvalds en 1991. L'architecture de Linux peut être décomposée en plusieurs couches, chacune remplissant un rôle spécifique dans le fonctionnement du système.

Linux n'est composé que de fichiers et de dossiers (ici appelé repertoire). Même les processus, etc...

- Noyau (Kernel) : Le noyau Linux est le cœur du système d'exploitation. C'est lui qui fait la communication entre la machine et le logiciel ;
- Réseau (Networking) : Linux dispose d'une architecture réseau robuste qui prend en charge divers protocoles de communication, tels que TCP/IP et UDP ;
- Systèmes de fichiers (File Systems) : Linux prend en charge différents systèmes de fichiers, tels que ext4, XFS, etc. Ces systèmes de fichiers organisent et gèrent le stockage des données sur les disques durs, les SSD et autres supports de stockage. Ils fournissent également des fonctionnalités avancées telles que la journalisation, la compression, la cryptographie, etc.

## Le système de fichiers

Au niveau de racine, le système est organisé sous la forme suivante...

- **Repertoires obligatoires**
  - `bin`: Binaires (comme des executables sous windows) des commandes essentielles
  - `boot`: Fichier static pour le programme d'amorçage (boot loader)
  - `dev`: Fichiers des pilotes de périphériques
  - `etc`: Configuration système du propre à la machine
  - `lib`: Bibliothèques partagées et modules noyau essentiel
  - `media`: Points de montage pour les support amovibles
  - `mnt`: Point de montage pour les montages temporaires
  - `opt`: Repertoires pour des logiciels optionnels / autres logiciels
  - `sbin`: Executables système essentiels
  - `srv`: Données pour les services fournis par le système
  - `tmp`: Fichiers temporaires
  - `usr`: Hiérarchie secondaire
  - `var`: Données variables
- **Repertoires facultatifs**
  - `home`: Répertoire personnel des utilisateurs
  - `root`: Répertoire personnel de l'utilisateur `root`

Le système de fichiers est représenté sous la forme d'un arbre.

Pour naviguer à travers celui-ci, on utilise...

- `.` (ou `./`) qui signifie "(dans) le dossier courant" ;
- `..` (ou `../`) qui signifie "(dans) le dossier parent" ;
- `~` qui redirige vers le répertoire personnel de l'utilisateur qui exécute la commande.
