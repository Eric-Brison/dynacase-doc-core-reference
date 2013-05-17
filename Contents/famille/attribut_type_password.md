# Type `password` {#core-ref:047a1bd7-b48a-4be3-907a-0e4f81d0162f}

## Description {#core-ref:b4d908e8-3758-4ab8-aceb-b1288ea666ae}

Les attributs de type *password* permettent d'insérer des valeurs sans en dévoiler le contenu.

## Représentation {#core-ref:0ea14a11-43ed-4b9f-904e-ce50b342079f}

*   consultation :
    
    La valeur avec les caractères remplacés par des étoiles.
    
    ![ password - consultation html ](famille/attributs/password-consultation.png "password - Consultation html")

*   modification :
    
    Un `input` de type `password`.
    
    ![ password - Modification html ](famille/attributs/password-modification.png "password - Modification html")

*   odt :
    
    Aucune représentation

## Comportement {#core-ref:9208756c-276a-42a3-aec4-eda84fec68e0}

En édition, le champ password est sytématiquement présenté vide. Lors de la sauvegarde, si la valeur est vide, alors l'ancienne valeur est conservée.

## Format de stockage {#core-ref:94e19ad3-ec9e-4d7f-b51e-8e26e08238e6}

La valeur stockée est la valeur brute.


Le type utilisé en base de donnée est `text`. 

## Options {#core-ref:5a79056c-6a6d-4f4c-91ea-1dfd257a8540}

[Options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496). 

Ce type d'attribut ne dispose d'aucune option spécifique.

