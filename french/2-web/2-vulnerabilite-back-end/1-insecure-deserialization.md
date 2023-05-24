# 1. Insecure Deserialization

## En quoi consiste cette attaque ?

Elle consiste à se servir d'une mauvaise vérification
de valeurs envoyés au serveur à travers une requête.

Le plus souvent, on s'en sert pour exécuter une commande
sur le serveur. On appelle cela du **Remote Code Execution** (RCE)

## Exemple avec un serveur web en Node.js

Considérons le code suivant écrit en JavaScript avec la librairie Express pour faire le serveur web.

```javascript
const getQuoteFromFortune = (defaultLength) => {
    // `fortune` est une commande pour générer des citations,
    // ici de longueur `defaultLength`.
    const { stdout } = child_process.execSync(`fortune -n ${defaultLength}`);
    return stdout;
};

// Renvoie la valeur de `value` passé dans le corps de la requête
// si cette valeur fais moins de 100 caractères.
// Sinon, on affiche une citation.
app.post("/api/echo_before_100", (req, res) => {
  const { value } = req.body;

  if (value.length < 100) {
    res.json({
      success: false,
      echo: value
    });
  }
  else {
    res.json({
      success: true,
      quote: getQuoteFromFortune(value.lenght)
    });
  }
});
```

Ici, on voit qu'à cause d'une faute de frappe et de la non vérification du type de `req.body.value`,
on peut exécuter n'importe quel commande que l'on veut sur le serveur.

En effet, on ne vérifie pas que `req.body.value` est bien du type `string`. Ainsi, on peut passer un objet
qui se sert de la faute d'orthographe dans le code `value.lenght`.

On pourrais ainsi envoyer au serveur, la requête suivante :

```jsonc
{
    "value": {
        "length": 150, // Pour déclencher le `else`.
        "lenght": "150; echo 'ma commande!'" 
    }
}
```

Ainsi, la valeur que retourne `getQuoteFromFortune(value.lenght)` sera `ma commande!`,
qu'on pourra récupérer dans `quote` de la réponse.

---

## [> 2. Injection SQL](./2-injection-sql.md)
