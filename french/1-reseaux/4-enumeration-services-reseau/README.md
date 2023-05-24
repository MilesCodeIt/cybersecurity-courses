# 4. Enumeration de services reseau

Énumérer les services exposés d'une machine dans un réseau peuvent nous permettre de trouver des vulnérabilités sur celle-ci.

Pour cela, nous allons utiliser `nmap`.

`nmap` (Network Mapper) est un scanner de ports libre. Il est conçu pour détecter les ports ouverts, identifier les services hébergés et obtenir des informations sur le système d'exploitation d'une machine, par exemple.


## Faire un scan des machines du réseau

> Pour les exemples qui vont suivre, on va prendre le réseau `192.168.1.0/24` pour
> une meilleure visualisation.

Cela nous permet d'identifier l'IP d'une machine sur le réseau.

```bash
nmap 192.168.1.*
```

*ou*

```bash
nmap 192.168.1.0/24
```

Les deux commandes font la même chose.

Si l'on veut juste faire un mini scan rapide, sans avoir aucune information sur les ports, on peut utiliser l'argument `-sn` qui désactive le scan des ports.

```bash
nmap -sn 192.168.1.*
```

## Export des résultats dans un fichier

> On utilisera un dossier `scans` pour les exports.

On peut utiliser l'argument `-oA` suivi de la destination du fichier.

```bash
nmap -oA ./scans/NOM_scan_initial IP_MACHINE 
```

## Scanner tout les ports.

On utilise les arguments `-p-` pour dire que l'on veut scanner tout les ports et `--open` pour demander à n'afficher que les ports ouverts et/ou possiblement ouverts.

```bash
nmap -p- --open -oA ./scans/NOM_full_tcp_scan IP_MACHINE
```

## Utiliser un script lors du scan

L'argument `--script` permet de définir le(s) script(s) que nmap va utiliser durant le scan.

```bash
nmap -sV --script=http-enum -oA ./scans/NOM_scrip_http_enum IP_MACHINE
```

## Scanner seulement des ports spécifiques en utilisant les scripts par défaut

Ici, on va scanner seulement les ports 22 et 80, en utilisant l'argument `-p`.

L'argument `-sC` revient à écrire `--script=default`.

```bash
nmap -sC -p 22,80 -oA ./scans/NOM_22,80_scan IP_MACHINE
```
