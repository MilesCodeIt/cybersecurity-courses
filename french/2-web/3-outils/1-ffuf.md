# 3. Identifier des ressources cachées avec `ffuf`

Premièrement, qu'est-ce que le "fuzzing" ?

C'est le processus d'envoyer pleins d'inputs aléatoire pour ainsi avoir des erreurs et/ou des sorties inattendues.

Pour *fuzz*, on aura toujours besoin d'une wordlist. Cette wordlist sera nos "inputs aléatoire".

## Usage de `ffuf`

On donne une wordlist à `ffuf` en utilisant l'argument `-w` et on utilise
la variable `FUZZ` pour définir où on veut utiliser cette wordlist.

### Brute forçage des chemins d'un site

```bash
# On utilise la wordlist sur tout les chemins d'un site
# internet pour essayer de trouver des URLs cachées.
ffuf -w ./ma-wordlist -u https://example.org/FUZZ
```

### Découverte de fichiers avec une extension spécifique

```bash
# On cherche les fichiers avec comme extensions, `php`, `text` et `html`.
ffuf -w ./ma-wordlist -u https://example.org/FUZZ -e .php,.txt,.html
```

### Brute forçage de requête POST

```bash
# On définit la méthode à utiliser avec `-X`
# On définit le corps de la requête POST avec `-d`
ffuf -w ./ma-wordlist -X POST -d “username=admin\&password=FUZZ” -u https://example.org/api/login
```

### Filtrage en fonction du code HTTP de la réponse

```bash
# On filtre uniquement les réponses `200` et `400` avec l'argument `-fc`
ffuf -w <path-wordlist> -u https://test-url/FUZZ -fc 200,400
```

---

## > [2. WordPress Analyzer (`wpscan`)](./2-wordpress-analyzer.md)
