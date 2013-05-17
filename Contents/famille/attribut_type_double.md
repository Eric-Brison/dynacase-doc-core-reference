# Type `double` {#core-ref:169365b9-7518-4222-b68c-5710d2779375}

## Description {#core-ref:b1aa4143-3e91-4911-bf98-f00c198552ef}

Les attributs de type *double* permettent d'insérer un nombre avec décimales.

## Représentation {#core-ref:e9b9d15c-0492-4664-8295-aa0f514bd020}

*   consultation :
    
    Le nombre, sans formatage
    
    ![ double - consultation html ](famille/attributs/double-consultation.png "double - Consultation html")

    Le formatage spécifique de *double* doit être conforme à celui utilisé dans la 
    fonction [sprintf][PHP_sprintf]. 
    Par exemple `double("%.03f")` pour avoir 3 chiffres maximum après la virgule.

*   modification :
    
    un `input` de type `texte` permettant de saisir le nombre.
    
    ![ double - Modification html ](famille/attributs/double-modification.png "double - Modification html")

*   odt :
    
    Le nombre, sans formatage
    
    ![ double - consultation odt ](famille/attributs/double-odt.png "double - Consultation odt")

## Comportement {#core-ref:38bb33db-6ee1-43e7-bd0f-a6f30a32638c}

Lors de l'enregistrement, le nettoyage suivant est effectué :

*   remplacement des `,` par `.`
*   suppression des espaces

La valeur nettoyée est validée au moyen de la fonction [is_numeric][PHP_is_numeric].

## Format de stockage {#core-ref:79669384-86c6-4b68-a8bc-bb1e87adc837}

La valeur stockée est la valeur nettoyée.

Le type utilisé en base de donnée est `double`. 
Si l'attribut est dans un tableau, le type en base donnée sera `text`.

## Options {#core-ref:f26a8f0c-f127-4f83-b036-a3172b8e1162}

[Options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496). 

Ce type d'attribut ne dispose d'aucune option spécifique.


<!-- links -->
[MDN_css_color_value]: https://developer.mozilla.org/en-US/docs/CSS/color_value "description du type css color sur MDN"
[MDN_css_length_value]: https://developer.mozilla.org/en-US/docs/CSS/length "description du type css length sur MDN"
[PHP_money_format]: http://php.net/manual/fr/function.money-format.php "documentation de money_format sur php.net"
[PHP_sprintf]: http://php.net/manual/fr/function.sprintf.php "documentation de sprintf sur php.net"
[PHP_is_numeric]: php.net/manual/function.is-numeric.php "documentation sur php.net"
[CKEDITOR_home]: http://ckeditor.com/ "Site officiel de CKEditor"
[CKEDITOR_option]: http://docs.cksource.com/ckeditor_api/symbols/CKEDITOR.config.html "options de CKEDITOR"
[SORTTABLEJS_home]: http://www.kryogenix.org/code/browser/sorttable/ "site officiel de sorttable.js"
[JSCOLOR_home]: http://jscolor.com/ "site officiel de JSColor"
[JSCALENDAR_HOME]: http://www.dynarch.com/projects/calendar/old/ "site officiel de JSCalendar"
[odt_restrictions]: #core-ref:3742b35d-ddc0-440e-a0aa-08ea2faf0e46