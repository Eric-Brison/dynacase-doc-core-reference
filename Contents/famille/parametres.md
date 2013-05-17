# Les paramètres de famille {#core-ref:4595c8e7-5002-4dbc-b6bb-882b4123efd8}

## Présentation {#core-ref:a69c36e0-dabd-46a3-a385-54116327111e}

Un paramètre de famille est une valeur stockée sur la famille directement,
et accessible depuis tous les documents de cette famille.

Ils sont assimilables à des propriétés de classe (ou propriétés statiques)
en programmation orientée objet, même si l'implémentation en diffère.

Ils peuvent être soumis à des contraintes.
Dans ce cas, la méthode doit être statique.

Un paramètre de famille peut également être dynamique,
lorsqu'il est défini par une méthode statique.
Dans ce cas, la méthode doit être statique et sera lancée à chaque récupération
du paramètre.

## Exemple d'utilisation {#core-ref:a29da8f2-6619-4b58-a3f2-a7c7690f0cb2}

Imaginons que l'on veuille calculer une référence unique pour tous les documents
de la famille *compte-rendu*. Cette référence doit être sous la forme
*[PREFIXE] - [chrono]* où *[PREFIXE]* est un préfixe commun à tous les documents,
et *[chrono]* est un numéro chrono (incrémenté de 1 à chaque nouveau document).

Le préfixe étant commun à tous les documents, on le stockera sous la forme d'un
paramètre de famille. Cela évite de devoir le stocker dans le code,
ce qui rend ce préfixe paramétrable sans redéploiement.