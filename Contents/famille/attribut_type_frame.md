# Type `frame` {#core-ref:62b8df9e-4418-4282-a2f2-63dc1306b717}

## Description {#core-ref:308b471c-0e6b-4e8e-879b-945495cf71a7}

Les attributs de type *frame* permettent de regrouper des attributs.
Ce regroupement sera le plus souvent sémantique.

## Représentation {#core-ref:ec628e98-b351-42b1-bed8-304b86755b1f}

*   consultation :
    
    un `div` entourant les attributs contenus dans cette frame. Le titre du cadre est dans une balise `div` placé avant le contenu.
    
    ![ frame - consultation html ](famille/attributs/frame-consultation.png "frame - Consultation html")

*   modification :
    
    un `fieldset` entourant les attributs contenus dans cette frame. Le titre du cadre est dans une balise `legend`.
    
    ![ frame - Modification html ](famille/attributs/frame-modification.png "frame - Modification html")

*   odt :
    
    Aucune représentation

## Comportement {#core-ref:0630b7d1-c83e-4379-9815-b9ec1f56490f}

Une frame est *collapsible* en cliquant sur son libellé.

## Format de stockage {#core-ref:2b4e60fd-609e-4d59-9acd-262bfac7de09}

Cet attribut n'est pas stocké.

## Options {#core-ref:7280d24d-8ece-41d2-9ef8-1643eb3e8b3b}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

bgcolor
:   Indique la couleur de fond du cadre.
    
    Les valeurs possibles sont :
    
    *   toute [couleur css valide][MDN_css_color_value]
        (exemple : `yellow`, `#FF335A`, etc.)



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