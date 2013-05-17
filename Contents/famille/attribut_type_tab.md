# Type `tab` {#core-ref:5b236ce8-ad99-4e21-ae8a-cbea6942c3e4}

## Description {#core-ref:a46a8c9a-4a1b-4552-8e14-2a3d78fc2cb8}

Les attributs de type *tab* permettent de créer des onglets.

## Représentation {#core-ref:06c83445-8009-4797-a9d7-de5fbe000b17}

*   consultation :
    
    Un onglet.
    
    ![ tab - consultation html ](famille/attributs/tab-consultation.png "tab - Consultation html")

    Note : Lors de l'impression d'un document, les onglets sont présentés comme des titres de paragraphes.
    
*   modification :
    
    Un onglet.
    
    ![ tab - Modification html ](famille/attributs/tab-modification.png "tab - Modification html")

*   odt :
    
    Aucune représentation

## Comportement {#core-ref:70e8dfaa-3aad-40ee-b2a9-503324fdc76c}

Aucun comportement particulier.

## Format de stockage {#core-ref:373f9b7d-07cb-48e9-8222-ada0d9eca6b6}

Cet attribut n'est pas stocké.

## Options {#core-ref:9e3801be-9cd1-4105-a271-787a7082b237}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

viewonfly
:   Indique que le contenu du tab est chargé en ajax lorsque l'utilisateur clique sur l'onglet.
    Cela réduit le temps de réponse pour les documents ayant de très nombreux attributs (plusieurs centaines).
    
    Cela n'est applicable que pour les vues utilisant la zone *FDL:VIEWBODYCARD*.
    Les actions utilisant cette zone sont :
    
    *   *FDL:FDL_CARD*,
    *   *FDL:IMPCARD*,
    *   *FDL:OPENDOC*,
    *   *FDL:VIEWEXTDOC*.
    
    Les valeurs possibles sont :
    
    *    `yes`
    *    **`no` (comportement par défaut)**

firstopen
:   Indique que cet onglet doit être sélectionné à l'ouverture du document.
    
    Cela n'est applicable que pour les vues utilisant les zones *FDL:VIEWBODYCARD* et *FDL:EDITBODYCARD*.
    Les actions utilisant cette zone sont :
    
    *   *FDL:FDL_CARD*,
    *   *FDL:IMPCARD*,
    *   *FDL:OPENDOC*,
    *   *FDL:VIEWEXTDOC*,
    *   *GENERIC:GENER
    
    Les valeurs possibles sont :
    
    *    `yes`
    *    **`no` (comportement par défaut)**



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