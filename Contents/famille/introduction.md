# Familles et documents {#core-ref:3ca3aeef-22a0-4e91-ad8b-357f2d05e227}
 
## Présentation {#core-ref:150d46d0-8925-4d79-9fb6-00a8a21f46df}

Dans Dynacase, le *Document* est la structure de base.
Le document est constitué d'attributs qui contiennent la donnée.

Un document est fortement structuré, c'est à dire que toutes les informations
qu'il contient sont typées et ordonnées.

Cette structure est définie par la famille : Une *famille* est un
*type de document* (Compte-rendu, Demande de congés, Véhicule, …).

Si on fait le parallèle avec la programmation orientée objet, alors on observe
les correspondances suivantes :

*   la *famille* est la *classe*,
*   le *document* est l'*instance*

Ainsi, dans Dynacase, toute manipulation d'information passera par une
manipulation de document :

1.  instanciation (depuis la base de données) ou création
2.  modification
3.  enregistrement

Ce chapitre présente les différents éléments de paramétrage permettant de
définir des familles de document. Chaque mécanisme est décrit dans sa propre
partie, alors que la dernière partie spécifie le format de définition
des structures.