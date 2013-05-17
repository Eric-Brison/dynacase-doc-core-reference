# Type `int` {#core-ref:ab21a433-c24f-40c2-99aa-321fdd1e81a3}

## Description {#core-ref:d66e4885-c1d5-41da-ba18-599d2ef37bea}

Les attributs de type *int* permettent d'insérer un nombre entier.

## Représentation {#core-ref:8342b998-5707-4d2d-9b47-ef2319e80fc7}

*   consultation :
    
    Le nombre, sans formatage.
    
    ![ integer - consultation html ](famille/attributs/integer-consultation.png "integer - Consultation html")

    Le formatage spécifique de *int* doit être conforme à celui utilisé dans 
    la fonction [sprintf][PHP_sprintf]. 
    Par exemple `int("%03d")` pour avoir 3 chiffres.

*   modification :
    
    Un input de type texte permettant de saisir le nombre.
    
    ![ integer - Modification html ](famille/attributs/integer-modification.png "integer - Modification html")

*   odt :
    
    Le nombre, sans formatage
    
    ![ integer - consultation odt ](famille/attributs/integer-odt.png "integer - Consultation odt")

## Comportement {#core-ref:eda3132e-f8a6-421b-ae07-d36615b705ec}

Lors de la sauvegarde, les vérifications suivantes sont faites :

*   Le nombre est un entier

## Format de stockage {#core-ref:b87a2fa8-a0ef-4835-908d-6ac777a72343}

La valeur stockée est la valeur brute du nombre.

Le type utilisé en base de donnée est `int`. 
Si l'attribut est dans un tableau, le type en base donnée sera `text`.

## Options {#core-ref:d4e4f0d4-8f92-44f2-8240-242ac98c00fe}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :



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
[PHP_sprintf]: http://php.net/manual/fr/function.sprintf.php "documentation de sprintf sur php.net"