# Les attributs {#core-ref:4e167170-33ed-11e2-8134-a7f43955d6f3}

## Présentation {#core-ref:61891ad3-b786-4824-bb31-f3cc209a96b6}

Les attributs correspondent à des *éléments de structure* du document.

Techniquement, ils correspondent à :

*   un champ de saisie en modification ;
*   une représentation textuelle en consultation ;
*   une colonne en base de données pour stocker la donnée.

Les attributs sont typés, et disposent d'options permettant de modifier leur
comportement, leur représentation, etc.

Cette partie présente chaque type d'attribut, décrit son usage, ses
représentations, et liste les options disponibles pour chacun de ces types.

Note sur les options : Dans Dynacase, les options sont *libres*, ce qui veut
dire que vous pouvez utiliser vos propres options pour rajouter des informations
sur certains attributs (par exemple, vous pourriez rajouter une option
*inSpecialView* pour lister les attributs à afficher dans votre vue spéciale).
De par leur nature extensible, les options n'ont pas de valeur par défaut ;
aussi, dans leur description, nous indiquerons par *(comportement par défaut)*
le comportement de l'option en l'absence de valeur.
