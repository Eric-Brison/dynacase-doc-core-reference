# Type `docid` {#core-ref:d461d5f5-b635-47a0-944d-473c227587ab}

## Description {#core-ref:c5d08a01-4cd2-4328-bce8-961ce6677d89}

Les attributs de type *docid* permettent de faire un lien vers un ou plusieurs documents. Ils sont appelés *relations*.

Les attributs de type *docid* sont *typés*, c'est à dire qu'on précise de quelle famille doivent être les documents cible.
Cela se fait au moyen de la syntaxe *docid("&lt;family>")* (Dans ce cas, les documents doivent être de la famille *&lt;family>* ou d'une de ses sous-familles).

## Représentation {#core-ref:ec18ef5f-f3fd-4ba4-b847-7f929cf694da}

*   consultation :
    
    Un hyperlien vers le document cible, avec comme label le titre du document cible, et l'icône du document
    
    ![ docid simple - consultation html ](famille/attributs/docid-simple-consultation.png "docid simple - Consultation html")

*   modification :
    
    une aide à la saisie vers les documents de la famille cible (et de ses sous-familles). L'aide à la saisie porte sur le titre uniquement, avec le filtre *contient, insensible à la casse*
    
    ![ docid simple - Modification html ](famille/attributs/docid-simple-modification.png "docid simple - Modification html")

*   odt :
    
    ![ docid simple - consultation odt ](famille/attributs/docid-simple-odt.png "docid simple - Modification odt")

## Comportement {#core-ref:75096496-f4e5-41c0-aa45-c02760723446}

Lors du rendu d'un docid, Dynacase récupère le titre des documents cibles.
Pour chaque document cible, si l'utilisateur n'a pas le droit de voir le document cible,
le titre est remplacé par le texte *Information non disponible* (se reporter à l'option *noaccesstext* pour personnaliser ce texte).

## Format de stockage {#core-ref:2f030503-257d-4f61-8edd-cb135fe74e53}

La valeur stockée est l'identifiant interne du document cible

Attention, malgré que l'identifiant soit majoritairement un nombre, son format d'enregistrement est un format texte.

Le type utilisé en base de donnée est `text`.

## Options {#core-ref:9bcfd205-fb07-4a71-be06-ba07d4a9cc7c}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

creation
:   Indique qu'un document de la famille de la relation pourra être créé depuis le formulaire.
    
    Dans ce cas, un bouton sera ajouté sur le formulaire.
    Ce bouton ouvre un formulaire de création de la famille cible.
    Lors de la sauvegarde du nouveau document, ce nouveau document est inséré dans le docid de départ.
    
    Pour les relations multiples, le nouveau document sera inséré dans la liste des documents.
    
    Lorsque la relation est déjà renseignée, le bouton permet de modifier le document cible au lieu d'en créer un nouveau.
    Si le document lié n'est pas accessible en modification, il sera alors affiché en consultation.
    De même, le bouton n’apparaîtra que si l'utilisateur a le droit en création sur la famille liée.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   un *objet (Attention: bien que cela y ressemble, ce n'est pas du JSON)* construit de la manière suivante :
        *   Pour définir la valeur d'un attribut du document cible : `attrid_document_cible: "valeur"` (si la valeur est fixe),
            ou `attrid_document_cible: attrid_document_source` si la valeur est à recopier depuis le document source.
        *   Pour fermer la fenêtre de création lors de la sauvegarde : `autoclose: "yes"`
        *   Pour appeler de nouveau l'aide à la saisie lors de l'insertion de la valeur dans le document source : `recallhelper: "yes"`
            
            Cela peut être utile dans le cas où l'aide à la saisie doit remplir plusieurs attributs du document source.
        
        Par exemple, `creation={an_name:CT, an_reference :"une référence", an_target:en_source, recallhelper: "yes", autoclose: "yes"}` indique que :
        *   l'attribut *an_name* prendra comme valeur initiale *la valeur  actuellement saisie par l'utilisateur dans le champ de l'aide à la saisie
        *   l'attribut *an_reference* prendra la valeur *une référence*
        *   l'attribut *an_target* prendra la valeur de l'attribut *en_source* du document source
        *   l'aide à la saisie sera rappelée lors de la sauvegarde du document nouvellement créé
        *   la fenêtre de création du nouveau document sera fermée lors de sa sauvegarde.

docrev
:   Indique quelle est la révision pointée par la relation.
    
    Les valeurs possibles sont :
    
    *   **`latest` (comportement par défaut)** : Dans ce cas, la relation pointe vers la dernière révision de la lignée documentaire ;
    *   `fixed` : Dans ce cas, la relation pointe vers la révision ayant l'id référencé ;
    *   `state(step)`, où *step* est une étape : Dans ce cas, la relation pointe vers le dernier document à l'étape *step*.
    
    Cette option affecte le comportement de l'aide à la saisie générée :
    
    *   lorsque l'option a la valeur *latest*, c'est l'initid du document qui est retourné ;
    *   lorsque l'option a la valeur *fixed*, c'est le docid de la dernière révision au moment de l'appel qui est retourné ;
    *   lorsque l'option a la valeur *state(step)*, seuls les documents à l'étape *step* sont listés,
        et c'est le docid de la dernière révision à l'étape step au moment de l'appel qui est retourné.

doctitle
:   Indique qu'un attribut contenant le titre du document cible doit être automatiquement renseigné.
    
    Cela est notamment utile pour la recherche plein texte, les tris, etc.
    
    Les valeurs possibles sont :
    
    *   **`no` (comportement par défaut)** ;
    *   tout id d'attribut existant : Dans ce cas, l'attribut référencé contient le titre du document cible ;
    *   `auto` : Dans ce cas, un attribut est généré (son id est *&lt;id_de_la_relation>_title* et son titre est *&lt;titre_de_la_relation> (titre)* )

isuser
:   Indique quels attributs sont utilisables pour le profilage des documents.
    
    Les valeurs possibles sont :
    
    *   `yes` : Dans ce cas, il faut que le document lié soit de la famille `IUSER` (Utilisateur)
        ou dérivé de `IUSER`.
    *   **`no` (comportement par défaut)**
    

multiple
:   Indique que plusieurs documents peuvent être référencés par la relation.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

noaccesstext
:   Indique le texte qui est affiché lorsque le document cible n'est pas visible.
    
    Cette valeur sera automatiquement ajoutée au catalogue de traduction.
    
    Les valeurs possibles sont :
    
    *   toute chaîne de caractères.
    
    En l'absence de l'option, le texte affiché est *Information non disponible*



<!-- links -->
[MDN_css_color_value]: https://developer.mozilla.org/en-US/docs/CSS/color_value "description du type css color sur MDN"
[MDN_css_length_value]: https://developer.mozilla.org/en-US/docs/CSS/length "description du type css length sur MDN"
[PHP_money_format]: http://php.net/manual/fr/function.money-format.php "documentation de money_format sur php.net"
[PHP_is_numeric]: php.net/manual/function.is-numeric.php "documentation sur php.net"
[CKEDITOR_home]: http://ckeditor.com/ "Site officiel de CKEditor"
[CKEDITOR_option]: http://docs.cksource.com/ckeditor_api/symbols/CKEDITOR.config.html "options de CKEDITOR"
[SORTTABLEJS_home]: http://www.kryogenix.org/code/browser/sorttable/ "site officiel de sorttable.js"
[JSCOLOR_home]: http://jscolor.com/ "site officiel de JSColor"
[JSCALENDAR_HOME]: http://www.dynarch.com/projects/calendar/old/ "site officiel de JSCalendar"
[odt_restrictions]: #core-ref:3742b35d-ddc0-440e-a0aa-08ea2faf0e46