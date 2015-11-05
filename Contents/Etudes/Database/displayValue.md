# Recherche de données affichées

Les données affichées ne sont pas les données recherchables.

Notamment se pose le cas des relations, des énumérés et des dates. 

En BD, c'est la valeur brute qui sert à la recherche. 

Pour contourner dans la plupart des cas le problème, c'est l'interface de saisie 
de la requête qui réalise un traitement préliminaire à la requête.

Lorsque le critère est "égal" la traitement suivant est réalisé :

Enuméré : Liste de choix d'énuméré : c'est la clef qui sert alors de critère
Docid : Choix d'un document: c'est l'id qui sert de critère
Date : Picker de date ( à faire ), c'est la date ISO qui sert de critère.


Par contre, il devient plus complexe de contourner cette limitation lorsque le critère
devient "contient", comme par exemple :

*   la date contient "10/2015"
*   ou pire la date contient "jeudi" 
*   l'énuméré contient "test"
*   le titre contient "hello"

Cela peut encore se régler en implémentant quelque jointure si le nombre de
condition n'est pas trop nombreux. Par contre, cela devient une requête assez
complexe et assez coûteux (en temps) lorsqu'il faut jointer plusieurs tables,
notamment une par condition.


Il faut savoir que l'enregistrement des données affichées ne suffira pas à
résoudre le problème. En effet, les données affichées sont fonction de la locale
de l'utilisateur et il est difficile d'envisager de doubler les enregistrements
de recherche par locale même si en absolu si on utilise les fonctions de
vectorisation il est nécessaire d'indexer en fonction de la langue du texte à
indexer.

