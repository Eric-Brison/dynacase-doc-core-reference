# Type `timestamp` {#core-ref:202b3080-ec86-47a6-8fe4-20e4cd5daa25}

## Description {#core-ref:315d0d73-d5ff-4c36-98ad-1985871abc2b}

Les attributs de type *timestamp* permettent d'insérer une date et heure.

## Représentation {#core-ref:bbed0319-c60a-4d4b-90c8-6523b134de52}

*   consultation :
    
    La date et heure formatée en accord avec la locale de l'utilisateur.
    
    ![ timestamp - consultation html ](famille/attributs/timestamp-consultation.png "timestamp - Consultation html")


    La date peut avoir un format particulier en utilisant la notation de [strftime][PHP_strftime].
    
    Exemple : `date("%A %e %B %y à %H heures %M minutes")` pour afficher
     `vendredi 17 mai 2013 à 15 heures 23 minutes`

*   modification :
    
    date picker avec possibilité de définir l'heure.
    
    ![ timestamp - Modification html ](famille/attributs/timestamp-modification.png "timestamp - Modification html")

*   odt :
    
    La date et heure formatée en accord avec la locale de l'utilisateur.
    
    ![ timestamp - consultation odt ](famille/attributs/timestamp-odt.png "timestamp - Consultation odt")

## Comportement {#core-ref:a4973455-217a-4988-a5d6-5e9b2d234243}

Lors de la saisie, la valeur est validée, c'est à dire que le format doit être :

*   soit au format « français » ;
*   soit au format « US » ;
*   soit au format ISO8601.

## Format de stockage {#core-ref:602096b5-9cd8-4d32-b217-6da24698f808}

La date est stockée au format ISO8601 « sans T » (yyyy-mm-dd hh:mm:ss).


Le type utilisé en base de donnée est `timestamp without timezone`. 
Si l'attribut est dans un tableau, le type en base donnée sera `text`.

## Options {#core-ref:a1d759de-e5df-48e7-8a77-7f1bd55b7c2a}

[options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496). 

Ce type d'attribut ne dispose d'aucune option spécifique.



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