# Type `time` {#core-ref:92319e61-3b3a-4a44-a884-30b4a8149f45}

## Description {#core-ref:1b4580f1-a501-44e1-a91c-1c723d0f1b8d}

Les attributs de type *time* permettent d'insérer une heure.

## Représentation {#core-ref:9d0e6897-6040-4a2a-a895-aa26e37d4a57}

*   consultation :
    
    La valeur brute.
    
    ![ time - consultation html ](famille/attributs/time-consultation.png "time - Consultation html")


    L'heure peut avoir un format particulier en utilisant la notation de [strftime][PHP_strftime].
    
    Exemple : `date("%H heures %M minutes %S secondes")` pour afficher
     `15 heures 23 minutes 04 secondes`

*   modification :
    
    2 inputs de type text, séparés par le symbole *:*.
    Du javascript transforme les entrées pour en faire des heures valides
    (les nombres sont remplacés par leur modulo respectif avec 24 et 60, et les autres valeurs sont remplacées par 00).
    
    ![ time - modification time ](famille/attributs/time-modification.png "time - Modification html")

*   odt :
    
    La valeur brute.
    
    ![ time - consultation odt ](famille/attributs/time-odt.png "time - Consultation odt")

## Comportement {#core-ref:fe20bd98-8ebb-47f2-8d26-b89ac794cc5c}

Lors de la sauvegarde, l'heure doit être comprise entre 0 et 23, 
les minutes entre 0 et 59 et les secondes facultatives entre 0 et 59.

La valeur est vérifiée, et doit correspondre à un des formats suivants :

*   .\d\d?:.\d\d?
*   .\d\d?:.\d\d?:.\d\d?

## Format de stockage {#core-ref:e99684cb-f7a4-4814-ac7d-d0e9365ed114}

La valeur stockée est la valeur nettoyée.

Le type utilisé en base de donnée est `time`. 
Si l'attribut est dans un tableau, le type en base donnée sera `text`.

## Options {#core-ref:a183ea74-26de-446b-93ab-587591bd2a57}

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
[PHP_strftime]: http://php.net/manual/fr/function.strftime.php "documentation de strftime sur php.net"