# 2. HTTP (HyperText Transfer Protocol)

Le protocole http est un protocole de communication client-serveur développé pour le World Wide Web.
Les clients les plus connue sont les navigateurs web.
La variante de HTTP protégée par les protocoles SSL ou TLS (SSL étant le prédécesseur de TLS) s'appelle HTTPS

## Implementation

Voici un exemple de requête http:

```http
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```

GET: Méthode utilisé

> Méthodes usuels:
>   - GET: Pour recevoir des informations
>   - POST: Pour envoyer des informations
>   - PUT: Pour modifier des informations
>   - DELETE: Pour supprimer des informations

/: chemin d'accès demandé

HTTP/1.1: protocole demandé

Le reste de la requête constitue les "headers" (entêtes). Elle rajoute des information a la requêtes comme par exemple l'URL du site auquel on veut communiquer (`host`)

Voici un exemple de réponse du serveur:

```http
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html>
<html>
    <...>
</html>
```

HTTP/1.1: version du protocole

200: code de réponse HTTP

OK: message de status

Le reste de la requête constitue, ici aussi, les "headers" (entêtes) dont une page web a la fin.

## Serveurs web usuels

- Apache
- nginx

Ils permettent de

## Code de réponses HTTP

### Succès

| Code | Description |
| ---- | ----------- |
| 200 OK | The request has succeeded. |

### Redirections

| Code | Description |
| ---- | ----------- |
| 301 Moved Permanently | The URL of the requested resource has been changed permanently |
| 302 Found | The URL of the requested resource has been changed temporarily |

### Erreur du client

| Code | Description |
| ---- | ----------- |
| 400 Bad Request | The server could not understand the request due to invalid syntax |
| 401 Unauthorized | Unauthenticated attempt to access page |
| 403 Forbidden | The client does not have access rights to the content |
| 404 Not Found | The server can not find the requested resource |
| 405 Method Not Allowed | The request method is known by the server but has been disabled and cannot be  used |
| 408 Request Timeout | This response is sent on an idle connection by some servers, even without any previous request by the client |

### Erreur côté serveur

| Code | Description |
| ---- | ----------- |
| 500 Internal Server Error | The server has encountered a situation it doesn't know how to handle |
| 502 Bad Gateway | The server, while working as a gateway to get a response needed to handle the  |request, received an invalid response
| 504 Gateway Timeout | The server is acting as a gateway and cannot get a response in time |
