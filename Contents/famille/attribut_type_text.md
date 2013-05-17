
# Type `text` {#core-ref:d68c1c48-b6ef-4654-a36f-67dfd68c38aa}

## Description {#core-ref:9a0de584-f3d3-4576-8070-36092184c53d}

Les attributs de type *text* permettent d'insérer du texte simple, sur une seule ligne.

## Représentation {#core-ref:6384b65b-e9b3-4e18-9ee4-586a20ea5820}

*   consultation :
    
    La valeur brute.
    
    ![ text - consultation html ](famille/attributs/text-consultation.png "text - Consultation html")

*   modification :
    
    un `input` de type `text`.
    
    ![ text - Modification html ](famille/attributs/text-modification.png "text - Modification html")

*   odt :
    
    La valeur brute.
    
    ![ text - consultation odt ](famille/attributs/text-odt.png "text - Consultation odt")

## Comportement {#core-ref:8a81d750-2fb2-40f7-926f-9710884bc5c7}

Lors de la sauvegarde, la valeur est nettoyée :

*   le caractère *"\r"* est remplacé par *" "* (espace).

## Format de stockage {#core-ref:ab1a2bea-df31-4e5a-9079-3a4f77c431d1}

La valeur stockée est la valeur nettoyée.

Le type utilisé en base de donnée est `text`.

## Options {#core-ref:92826f53-97a6-4fdb-a3cc-bb0b46877364}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

elabel
:   Valeur de l'attribut `@title` de l'`input` correspondant.
    
    Les valeurs possibles sont :
    
    *   Toute chaîne de caractères. Attention, la plupart des navigateurs n'acceptent pas de retour chariot.

esize
:   Valeur de l'attribut `@size` de l'`input` correspondant.
    
    Les valeurs possibles sont :
    
    *   Toute valeur entière.


