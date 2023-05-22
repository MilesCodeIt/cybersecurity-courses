# 2. Cross-Site Scripting (XSS)

Une injection HTML due à de mauvaises vérifications qui permet à n'importe qui d'insérer du code JavaScript dans la page HTML.

Il existe plusieurs type d'attaques XSS, ici on va se concentrer sur le `DOM XSS` qui
se passe lorsque le résultat d'une boite de dialogue donnée à l'utilisateur est directement écrit dans le HTML.

## Exemple de faille `DOM XSS`

```html
<div id="username-el"></div>
<button onClick="promptUser()">Cliquez pour entrer un nom d'utilisateur</button>
```

Si on affiche le contenu de l'article dans la `div` d'ID `username-el` sans prendre de précautions,
c'est à dire en utilisant directement `innerHTML`, on peut convertir le prompt de l'utilisateur en
éléments HTML.

On considère le code JS suivant :

```javascript
function promptUser () {
    const userInput = prompt("Entrez un nom d'utilisateur", "");
    document.getElementById("username-el").innerHTML = "Votre nom d'utilisateur est " + userInput;
}
```

Imaginons qu'on ait rentré `<h2>Hello</h2>`, par exemple, on peut voir que `Hello` est converti en titre, et donc, en élément HTML.

Bon, maintenant que l'on a vu qu'on peut faire cette injection HTML, on va essayer d'aller plus loin et d’exécuter du code JavaScript.

Si l'on rentre `#"><img src=/ onerror=alert(document.cookie)>`, on aura une pop-up qui contient nos
cookies sur le site sur lequel nous avons entré injecté cet élément `img`.

En effet, ici on abuse de l'attribut `onerror` qui exécute une fonction JS si l'image ne peut pas être
chargé. Ainsi, on rentre une source bidon pour que l'image ne charge jamais et notre fonction est toujours exécuté.

## Impact

Si un pirate mal intentionné arrive à trouver une faille XSS qui peut être permanente et visible à tous (stocké dans une base de données, par exemple), l'injection sera faite chez tout le monde.
Ainsi l'hacker peut en profiter pour récupérer les cookies et sessions de tout les utilisateurs pour voler des comptes.
