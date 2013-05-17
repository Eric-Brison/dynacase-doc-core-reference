# Type `account` {#core-ref:87230967-8155-421c-8bbe-70a3c1adc3c0}

## Description {#core-ref:f85a4012-c7e1-4a1f-bdaa-705b40e92114}

Les attributs de type *account* permettent de faire un lien vers un compte (utilisateur, groupe, ou rôle).

## Représentation {#core-ref:af7c88df-6eb7-4268-9ffa-532fe3cdee23}

*   consultation :
    Un hyperlien vers l'utilisateur cible, avec comme label le titre l'utilisateur cible, et son icone.
    
    ![ account simple - consultation html ](famille/attributs/account-simple-consultation.png "account simple - Consultation html")

*   modification :
    
    Une aide à la saisie vers les comptes.
    
    ![ account simple - Modification html ](famille/attributs/account-simple-modification.png "account simple - Modification html")

*   odt :
    
    Le titre du document cible.
    
    ![ account simple - consultation odt ](famille/attributs/account-simple-odt.png "account simple - Consultation odt")

## Comportement {#core-ref:9f3025e5-53e0-4b19-8e86-ff02b3ad035a}

Lors du rendu d'un *account*, Dynacase récupère dynamiquement le titre des documents cibles.
Pour chaque document cible, si l'utilisateur n'a pas le droit de voir le document cible,
le titre est remplacé par le texte *Information non disponible* (se reporter à l'option `noaccesstext` pour personnaliser ce texte).

## Format de stockage {#core-ref:cb3ffece-376a-4811-abe1-45c98f8dc9e4}

La valeur stockée est l'identifiant du document associé.

Le type utilisé en base de donnée est `text`.

## Options {#core-ref:87c874bb-7ed8-4aaa-b33b-897db020494f}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

group
:   Indique une restriction sur les comptes qui peuvent être référencés par la relation.
    
    L'aide à la saisie générée ne présentera que les comptes appartenant à ces groupes.
    
    Lorsque l'option *match* vaut *group*, seuls les sous-groupes des groupes référencés seront proposés.
    
    Cette option est incompatible avec *match=role*
    
    Les valeurs possibles sont :
    
    *   une liste de références de groupes (attribut *us_login*) séparés par des virgules

match
:   Indique une restriction sur les types de comptes qui peuvent être référencés par la relation.
    
    L'aide à la saisie générée ne présentera que les comptes dans les types listés.
    
    Les valeurs possibles sont :
    
    *   **`user` (comportement par défaut)**
    *   `group`
    *   `role`
    *   `all`

multiple
:   Indique que plusieurs documents peuvent être référencés par la relation.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

noaccesstext
:   Indique le texte qui est affiché lorsque le document cible n'est pas visible.
    
    Cette valeur sera automatiquement ajoutée au catalogue de traduction.
    
    Les valeurs possibles sont :
    
    *   toute chaîne de caractères (sur une seule ligne).

role
:   Indique une restriction sur les comptes qui peuvent être référencés par la relation.
    
    L'aide à la saisie générée ne présentera que les comptes ayant ces rôles.
    
    Les valeurs possibles sont :
    
    *   une liste de référence de rôles séparés par des virgules
