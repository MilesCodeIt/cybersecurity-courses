# 1. Exposition de données sensibles

<p align="center">
  <a href="#"># ></a>
</p>

---

L'exposition des données sensibles correspond aux données disponibles
à tout le monde dans une page HTML.

Voir la source d'une page web permet de voir les scripts appelés, les styles et principalement
le code HTML de la page.

> Pour voir ceci, on peut faire CTRL+U ou clique droit sur la page et "Voir la source".
> Sinon, on peut ajouter `view-source:` au début de l'URL (ex.: `view-source:https://google.com`)

Parfois, on peut trouver des commentaires contenant des identifiants ou autre donnée sensible.

## Exemple

```html
<form method="POST">
  <input type="text" name="username" />
  <input type="password" name="password" />

  <!-- TODO: Supprimer les identifiants admin:test de la base de données -->

  <button type="submit">Se connecter</button>
</form>
```

Comme on peut le voir ici, des identifiants ont été laissés par les développeurs, sûrement oubliés.

S'ils n'ont pas été encore supprimé de la base de données, on peut s'en servir pour s'authentifier
au compte `admin` avec le mot de passe `test`.
