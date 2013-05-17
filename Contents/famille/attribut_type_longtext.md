# Type `longtext` {#core-ref:88016225-a235-4dce-afdb-ea0c867a2cb4}

## Description {#core-ref:e39f3ea5-ee7a-476f-8b75-415434e46a8d}

Les attributs de type *longtext* permettent de saisir du texte multilignes, sans mise en forme.

## Représentation {#core-ref:b317d55d-7a36-4544-824b-a06bb480f721}

*   consultation :
    
    La valeur brute.
    
    ![ longtext - consultation html ](famille/attributs/longtext-consultation.png "longtext - Consultation html")

*   modification :
    
    Un textarea.
    
    ![ longtext - Modification html ](famille/attributs/longtext-modification.png "longtext - Modification html")

*   odt :
    
    La valeur brute.
    
    ![ longtext - consultation odt ](famille/attributs/longtext-odt.png "longtext - Consultation odt")

## Comportement {#core-ref:474b9011-0233-4bf5-ab1e-bc3289fcf35d}

Si un `longtext` est déclaré dans un tableau, les caractères `<BR>` sont remplacés par le caractère retour chariot `\n` lors de l'enregistrement.

## Format de stockage {#core-ref:d8153833-4f91-4a98-85d2-57610c1ff0d7}

La valeur stockée est la valeur brute.

Le type utilisé en base de donnée est `text`.


## Options {#core-ref:c1fe0afa-8bbe-4387-aa45-e52ffcbeb1f7}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

editheight
:   Indique la hauteur du `textarea` correspondant.
    
    Les valeurs possibles sont :
    
    *   une [taille css valide][MDN_css_length_value] (par exemple `400px`)
    
    La valeur par défaut est `2em`

elabel
:   Valeur de l'attribut `@title` du `textarea` correspondant.
    
    Les valeurs possibles sont :
    
    *   Toute chaîne de caractères. Attention, la plupart des navigateurs n'acceptent pas de retour chariot.


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