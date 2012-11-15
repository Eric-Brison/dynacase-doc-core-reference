# Action/introduction.md
 
La classe *Action* gère les actions des applications Dynacase.
Cette classe gère la sécurité, l'exécution et le rendu de l'action. Une action est toujours liée à une application. L'accès web à une action se fait via l'url : ?app=*APPLICATION_NAME*&action=*ACTION_NAME*.

Les propriétés de la classe *Action* sont :

## Propriétés de caractéristique
Ces propriétés sont pour la plupart issu du fichier ".app" de description de l'application.

id
: Identifiant numérique de l'action - Il est différent suivant les contextes car il est calculé en prenant le prochain numéro disponible lors de l'enregistrement de l'action

id_application
: Identifiant numérique de l'application portant l'action. Pour les mêmes raison que celles de l'*id* celui-ci est différent suivant les contextes.

name
: Référence de l'action. Contient le nom donnée dans le fichier "*.app*" de description de l'application.

short_name
: Description courte de l'action. Issu du fichier "*.app*" de description de l'application.

long_name
: Description longue de l'action. Issu du fichier "*.app*" de description de l'application.

script
: Nom du fichier PHP qui sera inclus lors de l'exécution de l'action. Il est issu du fichier "*.app*" de description de l'application si celui-ci est renseigné ou calculé s'il n'est pas renseigné. Dans ce dernier cas, le nom du script est le nom (*name*) de l'action en minuscule suivi de l'extension "*.php*". Le fichier PHP utilisé est celui inclus dans le répertoire de l'application (le nom du répertoire est le nom de l'application).

function
: Nom de la fonction PHP qui sera appelée lors de l'exécution de l'action. Il est issu du fichier "*.app*" de description de l'application si celui-ci est renseigné ou calculé s'il n'est pas renseigné. Dans ce dernier cas, le nom de la fonction est le nom (*name*) de l'action en minuscule.

layout
: Nom du fichier layout utilisé lors de l'exécution de l'action. Il est issu du fichier "*.app*" de description de l'application si celui-ci est renseigné ou calculé s'il n'est pas renseigné. Dans ce dernier cas, le nom du layout est le nom (*name*) de l'action en minuscule suivi de l'extension "*.xml*". Le fichier layout utilisé est celui inclus dans le sous-répertoire "*Layout*" du répertoire de l'application.

available
: Indique la disponibilité de l'action. Elle contient soit 'Y' soit 'N'. 'Y' indique que cette action peut être exécutée. Si cette propriété vaut 'N', l'action ne pourra être exécutée et un message d'erreur sera renvoyé à la place du résultat de l'action.

acl
: Nom du droit nécessaire pour exécuter l'action.

grant_level
: obsolète - non utilisé

openaccess
:  Indique que l'action peut être exécutée avec un jeton d'authentification sans demande de mot de passe. Elle contient soit 'Y' soit 'N' soit vide. L'accès avec jeton n'est autorisé que si la valeur est 'Y'.

root
: Indique que cette action est l'action principale de l'application. C'est celle qui sera lancée avec l'url "?app=*APPNAME*" sans préciser d'action. Elle contient soit 'Y' soit 'N'. L'action est déclarée principale si la valeur est 'Y'. Une seule des actions de l'application doit être principale.

icon
: icône de l'action. Non utilisé

toc
: Obsolète. Indique que l'action peut faire l'objet d'une présentation en onglets

toc_order
: Obsolète. Rang de l'action pour une présentation en onglets

father
: Obsolète. Non utilisé

## Propriétés fonctionnelles
Ces propriétés sont renseignées une fois que l'objet *Action* est initialisé avec un identifiant valide.

user
: Objet *Account* identifiant l'utilisateur courant

parent
: Objet *Application* identifiant l'application de l'action.

lay
: Objet *Layout* identifiant le Layout de repésentation de l'action

session
: Objet "Session" identifiant la session de paramètres de l'utilisateur courant.
