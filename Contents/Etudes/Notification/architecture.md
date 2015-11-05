# Architecture de la notification

La notification est basée sur le principe d'abonnement.

Un événement est envoyé et tout ce qui sont abonnés (à l'écoute) à cet événement
sont prévenus afin d'exécuter une tâche.


## Persistance des données

Les données des écouteurs et des événements sont stockés dans une base de
données. Cette base de données sera celle de Dynacase. Les différentes tables de
traitement seront créées sous un même schéma sql. Ceci permet d'éviter les
conflits avec les tables de Dynacase et permet plus facilement de séparer les
données.

## L'enregistrement des écouteurs

    [php]
    EventManager::addListener($listener)

Ces écouteurs sont enregistrés dans la base de données dans une table dédiée.


## L'envoi de l'événement

    [php]
    EventManager::dispatch($event)

Cette fonction enregistre les données de l'événement dans la base de données.
Elle vérifie que le programme de traitement des données est actif. Si ce n'est
pas le cas ce programme est activé.

L'événement en base à un status :

*   `new` (non consommé)
*   `activated` (en cours de traitement)
*   `done` (fini)

Un code d'erreur est aussi mis si le traitement s'est mal passé. De même des
éventuelles données de retour sont disponibles pour les programmes de
supervisions.


## Les traitements des notifications

Un seul programme de traitement est lancé. Il a comme fonction de dépiler les
événements à traiter et de les traiter un par un dans l'ordre d'arrivée.

Ce programme est un script `wsh` qui tourne en tâche de fond. L'utilisation d'un
`wsh` permet d'avoir un programme en php client et permet ainsi la capture de
signaux avec l'utilisation de la bibliothèque _pnctl_ de php.

Ce choix a été fait pour des raisons de maîtrise du périmètre de traitement et
d'efficacité du traitement de la notification. Dans ce cas, l'initialisation du
contexte est fait qu'une seule fois pour traiter plusieurs événements.

Ce programme enregistre le fait qu'il soit en vie. Pour
cela il verrouille un fichier (flock) avec son _pid_.


C'est cet indicateur de vie qui sera utiliser au `dispatch` pour savoir s'il
faut lancer un autre programme de traitement.

Ce programme traite les notifications en attente tant qu'il en a et dans une
certaine limite de temps. En effet, la consommation mémoire peut augmenter au
fur et à mesure des traitements à réaliser.

Ce programme s'arrête si :

1.   il est en fonctionnement depuis plus de _y_ secondes
2.   sa consommation mémoire a dépassé le max autorisé

Dans le premier cas, le programme se relance avant de s'arrêter s'il reste des
demandes à traiter.


![Cinématique de programme de traitement](notifarch.png)