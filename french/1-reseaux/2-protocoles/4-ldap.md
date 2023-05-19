# 4. LDAP (Lightweight Directory Access Protocol)

Le protocole LDAP s'agit d'un protocole ouvert et largement utilisé conçu pour accéder et gérer des services d'annuaire d'informations sur un réseau. LDAP est couramment utilisé pour l'authentification centralisée des utilisateurs, le stockage des informations utilisateur et l'organisation des données d'annuaire au sein d'une organisation.

LDAP fonctionne selon un modèle client-serveur, où le client envoie des demandes au serveur pour effectuer des opérations d'annuaire. Le serveur, également appelé serveur d'annuaire LDAP, détient les données d'annuaire et répond aux demandes des clients. Ces données d'annuaire comprennent généralement des informations telles que les profils d'utilisateurs, les appartenances à des groupes, les listes de contrôle d'accès et d'autres attributs.

LDAP offre une manière normalisée pour les applications et les services d'accéder aux services d'annuaire, permettant une intégration transparente et une interopérabilité entre différents systèmes. Il utilise une structure hiérarchique pour organiser les entrées d'annuaire, formant un arbre d'annuaire ou un arbre d'informations d'annuaire (DIT). Chaque entrée dans l'arbre a un nom distingué unique (DN) et contient des attributs qui définissent ses propriétés.

## Schema simplifié

```tree
- dc=example,dc=com (racine de l'arbre LDAP)
  |
  |-- ou=People (unité d'organisation pour les utilisateurs)
  |   |
  |   |-- cn=John Doe (entrée pour l'utilisateur John Doe)
  |   |   |
  |   |   |-- uid=johndoe
  |   |   |-- sn=Doe
  |   |   |-- givenName=John
  |   |   |-- mail=johndoe@example.com
  |   |
  |   |-- cn=Jane Smith (entrée pour l'utilisateur Jane Smith)
  |       |
  |       |-- uid=janesmith
  |       |-- sn=Smith
  |       |-- givenName=Jane
  |       |-- mail=janesmith@example.com
  |
  |-- ou=Groups (unité d'organisation pour les groupes)
      |
      |-- cn=Administrators (entrée pour le groupe Administrators)
      |   |
      |   |-- member=uid=johndoe,ou=People,dc=example,dc=com
      |   |-- member=uid=janesmith,ou=People,dc=example,dc=com
      |
      |-- cn=Managers (entrée pour le groupe Managers)
          |
          |-- member=uid=janesmith,ou=People,dc=example,dc=com
```

Dans cet exemple, l'arbre LDAP est basé sur le domaine fictif "example.com". La racine de l'arbre est représentée par "dc=example,dc=com". L'arborescence comprend deux unités d'organisation (ou) : "ou=People" pour les utilisateurs et "ou=Groups" pour les groupes.

Chaque utilisateur est représenté par une entrée (cn) sous "ou=People". Par exemple, l'utilisateur John Doe a une entrée avec les attributs uid, sn, givenName et mail.

Les groupes sont également représentés par des entrées (cn) sous "ou=Groups". Par exemple, le groupe Administrators a une entrée avec l'attribut member, qui fait référence aux utilisateurs faisant partie de ce groupe.

Cet exemple illustre une structure de base pour un arbre LDAP, mais dans la réalité, il peut être bien plus complexe en fonction des besoins et de l'organisation de données spécifique.
