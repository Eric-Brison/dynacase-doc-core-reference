# Routeur d'accès aux services web

Dynacase répond aux requêtes via le mécanisme d'action et application lorsque
le routeur "index.php" (par défaut) est utilisé.

Le module HTTP API, dispose d'un autre routeur qui en fonction de l'url et de
règles de routage basé sur l'url et la méthode HTTP de déclencher l'appel à une
méthode qui retourne des informations (pour l'instant principalement de la
donnée json).


|                          | index | api | guest | resizeimg | dav | authent | admin |
| ------------------------ | :---: | :-: | :---: | :-------: | :-: | :-----: | :---: |
| Droit d'accès            |   X   |     |   X   |           |  X  |         |   X   |
| Surcharge                |       |  X  |       |           |     |         |       |
| Mode authentifié         |   X   |  X  |       |     X     |  X  |         |   X   |
| Mode authentifié (jeton) |   X   |     |       |     X     |  X  |         |   X   |
| Mode non authentifié     |       |     |   X   |     X     |     |    X    |       |

L'avantage du routeur "index.php" est l'intégration d'un contrôle d'accès
configurable et administrable via le centre d'administration.

L'avantage du routeur "api.php" est la possibilité de surcharger les règles de
routages.

Le but est de pouvoir utiliser un routeur unique d'accès basé sur un système de
règles surchargeable comme pour le routeur "api".

Ces règles doivent être paramétrables pour intégrer la notion d'ACL comme le
fait le système d'action. Ces ACL n'étant plus liées à une application donnée
mais à une règle donnée. La même ACL pouvant être partagées par plusieurs
règles.

On retrouve alors dans ce routeur unique les avantages des 2 solutions mises en
œuvre.

Ce routeur doit aussi prendre en compte la partie authentification que ce soit
par mot de passe ou par jeton ou autre.

Ce routeur est donc configurable par l'administrateur pour indiquer quels sont
les systèmes d'authentification autorisées. Des systèmes d'authentification
standard (mot de passe) sont fournis par *Dynacase* tandis que d'autre peuvent
 être ajoutés par un tiers en programmant un système personnalisé
d'authentification.

Les interfaces permettant de construire un système d'authentification sont à
définir. Dynacase propose déjà un mécanisme d'authentification. Celui-ci devra
être repris afin d'avoir un système plus homogène et plus ouvert. Ceci à un
impact sur les comptes (voir autre §account)

