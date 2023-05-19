# 4. Enumeration de services reseau

Énumérer ces services peuvent nous permettre de trouver des applications vulnérables sur la machine victime.

## L'outils principal: NMap

### Description

NMap (Network Mapper) est un scanner de ports libre. Il est conçu pour détecter les ports ouverts, identifier les services hébergés et obtenir des informations sur le système d'exploitation d'un ordinateur distant.

### Utilisation

```bash
nmap -sV --open -oA ./scans/{fichiers_de_sortie}_scan_initial {IP} 
```

=> Scanne les 100 ports les plus souvent ouvert.

```bash
nmap -p- --open -oA ./scans/{fichiers_de_sortie}_full_tcp_scan {IP} 
```

=> Scanne tous les port pour être sur d'en louper aucun.

```bash
nmap -sC -p 22,80 -oA ./scans/{fichiers_de_sortie}_script_scan {IP} 
```

=> Scanne les ports 22 et 80 en utilisant les scripts par default.

```bash
nmap -sV --script=http-enum -oA ./scans/{fichiers_de_sortie}_nmap_http_enum {IP}
```

=> Scanne en utilisant le script http-enum
