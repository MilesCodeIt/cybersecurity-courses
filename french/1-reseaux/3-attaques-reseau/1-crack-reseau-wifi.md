# 2. Crack de réseaux Wi-Fi

Dans ce cours, nous allons nous intéresser seulement au WPA/WPA2 pour éviter de trop s'étaler sur la durée.

## Comment ça fonctionne ?

À chaque fois que vous vous connectez sur un réseau Wi-Fi, un "handshake" est envoyé de votre appareil au routeur.

Ce handshake contient le mot de passe encrypté qu'on ne peut pas décrypter.

Cependant, ce que nous pouvons faire, c'est tout simplement utiliser une "wordlist"
et encrypter chaque entrée puis la comparer avec le mot de passe encrypté du handshake.

Lorsqu'on trouve une correspondance entre les deux, on détermine ainsi le mot de passe du réseau.

## Démonstration pour un réseau WPA/WPA2 PSK

### Prérequis

#### Appareil "attaquant"

L'appareil que l'on va utiliser pour faire l'attaque doit avoir une carte Wi-Fi
qui supporte le mode `monitor`. Pour vérifier cela, on peut exécuter `iw list` et vérifier si `monitor`
est présent dans `Supported interface modes`.

Dans notre cas, nous allons utiliser une Raspberry Pi 4B avec l'image de Kali Linux d'installé.

Il faut savoir que pour supporter le mode `monitor` sur une RPi, il faut avoir un patch qui est préinstallé
dans cette image Kali Linux.

#### Appareil "cible"

Cet appareil doit être déjà connecté au réseau, c'est "grâce" à lui qu'on va
récupérer le handshake.

#### Un réseau Wi-Fi configuré en WPA/WPA2 PSK

Le réseau qu'on va attaquer. L'appareil "cible" doit être connecté dessus pour simplifier la procédure.

### Passer son interface réseau en mode `monitor` sur l'appareil "attaquant"

On va utiliser la commande `airmon-ng` pour démarrer le mode `monitor` sur l'interface `wlan0`.

> À noter que le nom de l'interface Wi-Fi peut changer en fonction de l'appareil,
> on peut la récupérer avec la commande `ip addr`.

```bash
sudo airmon-ng start wlan0
```

Maintenant, on va tuer les processus qui pourraient interférer avec notre interface.

On peut faire ceci avec la commande prévue à l'effet...

```bash
sudo airmon-ng check kill
```

> Note: Notre interface `wlan0` à maintenant changé de nom.

On peut vérifier le fait que notre interface est bien en mode `monitor` en utilisant `iwconfig`.

```console
$ iwconfig
...
wlan0mon    ... Mode:Monitor ...
...
```

### Récupérer le BSSID du réseau qui nous intéresse

On va utiliser la commande `airodump-ng` pour obtenir une liste des réseaux
disponibles proche de nous depuis notre interface Wi-Fi.

```bash
sudo airodump-ng wlan0mon
```

On identifie le nom du réseau grâce au ESSID.

Ce qui nous intéresse ici, est le **BSSID** et le channel **CH**, qu'il faudra noter pour la prochaine partie.

### Récupérer un handshake

> Imaginons que le BSSID que nous avons repéré est `BS:SS:ID:AA:BB:CC` et que le channel que nous avons pu récupérer est `1`.

Nous pouvons maintenant obtenir une liste des appareils connectés au réseau, toujours en utilisant `airodump-ng`

```bash
sudo airodump-ng -d BS:SS:ID:AA:BB:CC -w nom_du_fichier_export -c 1 wlan0mon
```

Ici, `-d` correspond au BSSID, `-w` le fichier contenant le handshake qu'on va récupérer et `-c` le channel obtenu précédemment.

Maintenant, si vous vous souvenez, pour obtenir un handshake, il faut qu'un appareil se connecte au réseau.
Vu que cela peut prendre du temps, on peut accélérer le processus en envoyant des packets de déconnexion vers un appareil, l'appareil "cible".

Ainsi, on peut ouvrir un nouveau terminal pour essayer de forcer un appareil à se déconnecter du réseau - on part du principe que l'appareil va automatiquement se reconnecter au réseau.

```bash
sudo aireplay-ng -0 0 -a BS:SS:ID:AA:BB:CC -c AA:BB:CC:DD:EE:FF wlan0mon
```

`-0` veut dire que les packets qu'on veut envoyer sont ceux pour la déconnexion (deauth).
Le `0` en valeur de `-0` veut dire qu'on envoie un nombre indéterminé de packets.
`-a` est l'adresse du routeur et `-c` est l'adresse de l'appareil "cible".

On laisse tourner jusqu'à ce qu'on ait `WPA handshake: AA:BB:CC:DD:EE:FF` dans la première ligne de notre premier terminal.
Lorsque ce message s'affiche, ça veut dire que vous avez capturé un handshake.

Vous pouvez maintenant fermer tout les terminaux.

### Cracker le mot de passe en utilisant le handshake capturé

Nous pouvons constater la création de plusieurs fichiers dans le dossier où la commande a été exécuté.

Celui que nous utiliserons sera celui qui se termine par l'extension `.cap`.

Pour cracker le mot de passe, nous allons utiliser la commande `aircrack-ng`.

```bash
aircrack-ng -w ./maWordList.txt ./monFichier.cap
```

Maintenant, vous pouvez attendre jusqu'à avoir une `"KEY FOUND"` !
