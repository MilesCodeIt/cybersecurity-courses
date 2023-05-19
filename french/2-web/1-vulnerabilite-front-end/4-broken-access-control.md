# 4. Faille dans le contrôle d'accès (Broken Access Control)

Accès à des fonctions dont on est sensé en avoir l'accès dans l'application web.

## Exemple

Imaginez un blog où tout le monde peut écrire des articles.
Chacun peut écrire un article sur son compte dans le blog et personne ne peut éditer les articles
des autres.

Lorsque vous supprimez un de vos article, vous remarquez cette URL: `http://example.org/api/articles/delete?id=5`.

Cela veut dire plusieurs choses :
    - Chaque article doit avoir un ID unique ;
    - L'article que vous avez supprimé avait un ID de `5`.

Maintenant, vous vous demandez ce qu'il se passe si seulement on changeait cet ID dans l'URL !

Si il y a une faille dans le contrôle d'accès, cela vous permettrez de supprimer n'importe quel
article tant que vous donnez l'ID de celui-ci.
