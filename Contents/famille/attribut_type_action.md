# Type `action` {#core-ref:a372b25d-ac8f-4b18-854c-6081bf5d64ae}



## Description {#core-ref:a3a60027-5120-4dc9-86d3-fd806ca130b2}

Les attributs action permette d'ajouter des boutons dans les interfaces de consultation. Ces boutons déclencheront l'action défini par l'attribut.

## Représentation {#core-ref:73c8d899-10b6-4caf-a980-558e45a6e25e}
*   consultation :
    
    Un bouton placé en bas du document.

*   modification :
    
    Non représenté

*   odt :

    Non représenté

## Comportement {#core-ref:e034ec11-9e86-422a-a94f-38c67ab5bbf3}

Si l'utilisateur peut exécuter l'action alors le bouton est présenté.

## Format de stockage {#core-ref:f527a787-bf29-46dc-9ce2-f8c19485e31a}

Cet attribut n'est pas stocké.

## Options {#core-ref:90002286-c6f9-47b3-8183-2ad575d4d566}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

batchfolder
:   Indique si l'action définie doit être appliquée sur tous les éléments du dossier.
    
    Option utilisable uniquement dans les familles dérivées de la famille *EXEC* (Traitement).
    Se reporter à la documentation de la famille *Traitement* pour plus de détails.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

