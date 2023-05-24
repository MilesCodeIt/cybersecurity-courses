# 1. Images

Les images sont très importante en Osint. Il existe different moyens d'obtenir des information a partir d'une image.

## Données EXIF

L’Exchangeable image file format ou EXIF est une spécification de format de fichier pour les images utilisées par les appareils photographiques numériques.

Les données EXIF constituent un remplacement commode du petit carnet qui accompagnait, à l'époque de la photographie chimique, les photographes méticuleux. Sur les appareils numériques, elles sont conservées automatiquement avec chaque photo.

Les balises de métadonnées définies dans le format EXIF standard couvrent un large éventail de données, dont :

- Information de la date et de l’heure. Les appareils numériques enregistrent la date et l’heure de la prise de vue et l’insèrent dans les métadonnées ;
- Les réglages de l’appareil. Cela comprend des informations statiques telles que la marque et le modèle de l’appareil et des informations variables telles que l’orientation, l’ouverture, la vitesse d’obturation, la longueur de focale, la sensibilité…
- Des informations géographiques provenant d’un éventuel système GPS connecté à l’appareil. En 2008, de plus en plus d'appareils gèrent cette fonction. Certains photographes utilisent un système classique pour localiser leurs déplacements puis ajoutent manuellement aux métadonnées les coordonnées géographiques correspondant aux données temporelles de la photographie ;
- Description et information des droits d’auteur.

Acceder à ces donnés est très simple. Sur windows il suffit de faire `fichier > clique-droit > propriétés > details`. Sur linux il existe une commande `exif`. Sinon il existe de nombreuses ressources en ligne.

## Recherche inversé d'images Google

Google image nous permet de faire une recherche inversée d'image, c'est-à-dire qu'on peut retrouver la provenance d'une image

## [Tineye](https://tineye.com/)

Tineye fait comme la recherche inversé d'images Google en plus puissant. Il donne plus de détails ainsi que des réseaux sociaux.
