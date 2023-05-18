# 2. Fondamentaux de Linux

Une fois dans le terminal, vous avez une quasi infinité de possibilité!
Voici une liste, avec des exemples, de commandes que vous allez utiliser régulièrement dans ce cours.

- `whoami` : donne le nom de l’utilisateur que vous utilisez.
- `echo` : affiche le texte qu’on lui passe.
    on peut écrire dans un fichier en utilisant `>` : `echo Hello > fichier.txt`
- on peut savoir où on est actuellement en utilisant la commande `pwd`
- `ls` : permet de lister les fichiers dans le dossier où nous sommes actuellement
    on peut lister les fichiers d’un dossier spécifique en le passant en argument `ls ./leNomDuDossier`
- `cd nomDuDossier` : permet de naviguer dans `nomDuDossier`
- `cat fichier.ext` : permet d’afficher le contenu d’un fichier.
- `mkdir nomDuDossier` : crée un dossier `nomDuDossier`
- `rm fichier.ext` : permet de supprimer un fichier
- `rmdir nomDuDossier` : permet de supprimer un dossier (vide)
- `rm -rf` pour supprimer de façon récursive
- `mv fichier1 fichier2` : permet de déplacer `fichier1` en `fichier2` (ici on renomme le fichier)
- `mv fichier1 ./dossier/` : ici on déplace `fichier` dans `dossier`
- `cp fichier1 fichier2`: le fonctionnement est pareil que celui de `mv` sauf qu’à la place de déplacer, on copie.
- `grep keyword fichier.ext`: retourne la ligne contenant le keyword
    peut aussi être utilisé avec `|`, par exemple: `cat fichier.txt | grep keyword`
- `wc fichier.ext`: compte le nombre de caractère d’un fichier
