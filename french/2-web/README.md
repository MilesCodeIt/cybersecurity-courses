# 2. Web

<p align="center">
  <a href="../1-reseaux/README.md">< chapitre des réseaux</a> - <a href="#">chapitre d'après ></a>
</p>

## Introduction au chapitre

Nous allons aborder dans ce chapitre: les applications web et les sites web.

Une application web est une application interactive qui s'exécute sur les navigateurs web, tel que Chrome, Firefox, etc...

Les applications web adoptent généralement une architecture client-serveur (front-end/back-end) pour exécuter et gérer les interactions des utilisateurs.

Cela permet d'héberger des applications puissantes avec un contrôle en temps réel quasi complet sur leur conception et leurs fonctionnalités tout en étant accessibles dans le monde entier.

On a quelques exemples d'applications web typiques comme GMail, Amazon ou Google Docs.

De nos jours, il n'est pas très courant de trouver un hôte disponible de l'extérieur directement exploitable via un exploit public connu, mais pourtant cela arrive.

On peut parfois trouver une faille qui permet l'execution de code, ou tout simplement une injection SQL.

## Sommaire

1. Vulnérabilités front-end
    1. [Exposition de données sensibles](./1-vulnerabilite-front-end/1-exposition-de-donnees-sensibles.md)
    2. [Cross-Site Scripting (XSS)](./1-vulnerabilite-front-end/2-xss.md)
    3. [Cross-Site Request Forgery (CSRF)](./1-vulnerabilite-front-end/3-csrf.md)
    4. [Faille dans le contrôle d'accès (Broken Access Control)](./1-vulnerabilite-front-end/4-broken-access-control.md)

2. Vulnérabilités back-end
    1. Insecure Deserialization (ex: !type checking => req.body command injection)
    2. Broken Authentication (ex: SQL Injection)
    3. Security Misconfiguration // apachd -> .htaccess (cgi-bin)
    4. Using Libraries with Known Vulnerabilities // Lib -> flat (prototype pollution)

3. Outils
    1. [Identifier des ressources cachés avec `ffuf`](./3-outils/1-ffuf.md)
    2. [Analyser des sites WordPress avec `wpscan`](./3-outils/2-wordpress-analyzer.md)
    3. [Intercepter et modifier des requêtes avec Burp](./3-outils/3-burp-suite.md)
