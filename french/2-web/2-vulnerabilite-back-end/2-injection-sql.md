# 2. Injection SQL

## En quoi consiste cette attaque ?

Comme son nom l'indique, elle consiste à injecter du code SQL dans une requête.

## Un exemple de code vulnérable en PHP

```php
$link = // ...

$username = $_POST["username"];
$password = $_POST["password"];

$sql = "SELECT id, username FROM users WHERE username = '$username' AND password = md5('$password')";
$result = mysqli_query($link, $sql);

if (mysqli_num_rows($result) > 0) {
    session_start();
    $_SESSION["loggedin"] = true;
}

mysqli_close($link);
```

Ici, on peut facilement se connecter sur n'importe quel compte en injectant du code SQL dans la variable `username`.

La première idée qui peut venir en tête est quelque chose du style `admin' --`. On récupère l'entrée avec le nom
d'utilisateur `admin` et on met en commentaire le reste du code SQL en utilisant `--` pour supprimer la vérification du mot de passe.

Ainsi, la requête SQL exécutée sera `SELECT id, username FROM users WHERE username = 'admin'`.

## Démonstration avec OWASP Juice Shop

> On se servira de ce site internet pour notre démonstration, <https://demo.owasp-juice.shop/#/login>.

Nous voici en face d'une page de login, où l'on doit s'identifier.

Pour ce faire, nous allons faire un peu la même chose que dans la section [précédente](#un-exemple-de-code-vulnérable-en-php).

### Inspection

Premièrement, nous allons ouvrir les outils de développeur de notre navigateur et inspecter les requêtes
qui sont émises pour s'authentifier. On va donc entrer un identifiant/mot de passe quelconque pour inspecter la requête.

On peut constater une requête POST vers `https://demo.owasp-juice.shop/rest/user/login`
avec le payload suivant:

```json
{
    "email": "test@example.org",
    "password": "12345678"
}
```

La réponse donne: `Invalid email or password.`

### Injection SQL

On peut tester si il y a une vulnérabilité SQL en tentant de faire une requête en mettant un `'` ou `"`
dans l'`email`.

Lorsque l'on fait une requête avec l'email: `'`, on obtient une réponse différente:

```json
{
    "error": {
        "message": "SQLITE_ERROR: unrecognized token: \"25d55ad283aa400af464c76d713c07ad\"",
        "stack": "Error....",
        "name": "SequelizeDatabaseError",
        "parent": {
            "errno": 1,
            "code": "SQLITE_ERROR",
            "sql": "SELECT * FROM Users WHERE email = ''' AND password = '25d55ad283aa400af464c76d713c07ad' AND deletedAt IS NULL"
        },
        "original": {
            "errno": 1,
            "code": "SQLITE_ERROR",
            "sql": "SELECT * FROM Users WHERE email = ''' AND password = '25d55ad283aa400af464c76d713c07ad' AND deletedAt IS NULL"
        },
        "sql": "SELECT * FROM Users WHERE email = ''' AND password = '25d55ad283aa400af464c76d713c07ad' AND deletedAt IS NULL",
        "parameters": {}
    }
}
```

Comme nous pouvons le voir, nous venons de créer une erreur dans la requête SQL. Ainsi,
nous savons maintenant que cette application est vulnérable à l'injection SQL.

Vu que l'on peut avoir la requête SQL complète dans l'erreur, on peut facilement
créer une injection qui nous permet de nous authentifier: `' OR TRUE --`

Ici, on utilise `'` pour sortir de la condition de l'email et on ajoute `OR TRUE` qui permet de
rendre la condition toujours vraie.

`--` est utilisé pour mettre en commentaire le reste de la requête SQL, ainsi la condition
finale dans le `WHERE` sera `email = '' OR TRUE` qui est donc toujours vrai.

### Avec quel compte sommes nous identifié ?

On peut retourner dans le menu et voir que nous sommes identifié, par chance, sur le compte administrateur !
