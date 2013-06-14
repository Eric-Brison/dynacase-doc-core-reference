# Applications, actions et ACL {#core-ref:a88e69b9-b583-4651-898f-d2583d0eeb1f}

## Résumé {#core-ref:7fcd8c91-b981-4ef6-b4b5-7975a17dbe73}

Toute requête effectuée sur le serveur exécute une action d'une application.
L'action détermine la fonctionnalité attendue par la requête.

Vocabulaire :

Application
:   Une application est un conteneur permettant de regrouper des *Actions*, 
    des *ACL* et des *paramètres*.

Action 
:   Une action est une fonction PHP. Cette fonction peut utiliser
    l'ensemble de l'API de Dynacase et est exécutée au nom de l'utilisateur en cours
    (les droits, visibilités et autres sont donc respectés). Elles peuvent être
    utilisées pour effectuer :
    
    * des exports particuliers (textuel ou binaire),
    * des traitements particuliers (dupliquer des documents, effectuer des 
        modifications de groupes, créations automatiques, etc.),
    * des IHM spécifiques (mise en place d'un portail d'accueil, d'interface 
      de manipulation de documents, etc.)

ACL
:   Une ACL est un droit applicatif, elle a deux usages complémentaires. Au 
    niveau d'une action, elle indique que l'utilisateur doit posséder cette ACL
    pour pouvoir utiliser cette action et associée à un compte 
    (rôle, utilisateur, groupe) elle indique que ce compte possède cette ACL.

## Application {#core-ref:82e2587e-fe2b-49ce-a4aa-a25fdc9c12c2}

Une application est caractérisée par :

Des propriétés
:   Ces propriétés permettent d'identifier et de caractériser l'application. Il y a notamment :
    
    Nom logique
    : C'est le nom logique de l'application, il est utilisé lors de son appel.
    
    Nom
    : Ce nom est utilisé dans les interfaces d'administration, il peut-être traduit.
    
    Description
    : Cette description est utilisée dans les interfaces d'administration, elle peut-être traduite.
    
    Icône
    : Cette icône est utilisée dans les interfaces d'administration.

Une liste d'ACL
:   Cette liste est sous la forme d'un tableau PHP d'ACL. Elle est propre à chaque application

Une liste de définition d'action
:   Cette liste est présentée sous la forme d'un tableau PHP d'action. La liste des actions est propre à chaque application.

Des paramètres applicatifs
:   Les paramètres applicatifs sont présentés sous la forme d'une liste décrivant l'ensemble des paramètres applicatifs applicables pour l'application

NB : une application peut hériter d'une autre, elle hérite alors de son
paramétrage et des actions et paramètres applicatifs.

## ACL {#core-ref:5afe50d4-321c-4dd7-ac1c-9fc3a5076e52}

Une ACL est un marqueur permettant d'indiquer que :

* un droit est nécessaire pour effectuer une action,
* un compte le possède et pourra donc effectuer les actions nécessitant l'ACL.

La vérification des ACL est incluse dans la plate-forme et est effectuée automatiquement lors de l'appel à une action. Si le compte utilisé pour faire l'appel ne possède pas l'ACL nécessaire un message d'erreur est alors généré.

## Action {#core-ref:5f3cfda3-6293-4b3b-8b9f-616e9f9b029f}

L'action est constituée d'une fonction PHP qui est utilisée lors de son appel.

Les principaux éléments constituant une action sont :

Un nom logique
:   Il est utilisé pour référencer l'action, notamment, lors de l'appel de l'action.

Le nom logique d'une ACL (facultatif)
:   S'il est présent la plate-forme n'exécute l'action que si le compte demandant l'exécution possède l'ACL.

Un nom de layout (facultatif)
:   Il permet d'indiquer avec quel layout (template utilisé par le moteur de template) l'action est rendue (par défaut, le template a le même nom que l'action).
    NB : si l'action n'a pas de représentation, ou renvoie un élément encodé (JSON, base64, etc.), il est possible d'indiquer à l'action de ne pas utiliser le moteur de template.

## Paramètre applicatif {#core-ref:b8021fc2-a764-43b2-b5db-a12406363650}

Un paramètre applicatif est un élément que l'on peut ajouter à une action pour stocker des données permettant de paramétrer l'action. Une fois le paramètre enregistré une API permet de le manipuler (récupérer, modifier sa valeur).  
De plus, les paramètres applicatifs sont présentés via les interfaces d'administration de Dynacase et peuvent être modifiés par les administrateurs système. Il sont utilisés principalement dans deux cas :

* mettre en place une persistance au niveau d'une application pour l'ensemble des utilisateurs (par exemple le format du préfixe du nom de fichier que retourne une action d'export),
* mettre en place une persistance au niveau d'un utilisateur d'une application (par exemple les préférence d'export de l'utilisateur en cours).

Les principaux éléments constituant d'un paramètre applicatif sont :

Un nom logique
:   Il permet de manipuler le paramètre applicatif.

Une valeur par défaut
:   Elle est utilisée pour initier la valeur du paramètre.

Une visibilité
:   Elle indique si un paramètre applicatif est ou pas commun à l'ensemble des utilisateurs.
