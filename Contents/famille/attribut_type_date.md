# Type `date` {#core-ref:7ed5e5fe-2b68-489b-b720-58b3f465f20b}

## Description {#core-ref:d30f37bb-a907-4ce8-a09e-dc6bff21b76b}

Les attributs de type *date* permettent d'insérer une date.

## Représentation {#core-ref:a08547fe-6459-48a2-b94b-747f70e91219}

*   consultation :
    
    La date formatée en accord avec la locale de l'utilisateur.
    
    ![ date - consultation html ](famille/attributs/date-consultation.png "date - Consultation html")
    
    La date peut avoir un format particulier en utilisant la notation de [strftime][PHP_strftime].
    
    Exemple : `date("%A %e %B %y")` pour afficher `vendredi 17 mai 2013`

*   modification :
    
    Un date picker (basé sur [JSCalendar][JSCALENDAR_HOME]).
    
    ![ date - Modification html ](famille/attributs/date-modification.png "date - Modification html")

*   odt :
    
    La date formatée en accord avec la locale de l'utilisateur.
    
    ![ date - consultation odt ](famille/attributs/date-odt.png "date - Consultation odt")

## Comportement {#core-ref:240a15ae-1a7d-4c97-bc58-3fd9533bc02f}

Lors de la saisie, la date est validée, c'est à dire que le format doit être :

*   soit au format « français » ;
*   soit au format « US » ;
*   soit au format ISO8601.

## Format de stockage {#core-ref:87c42468-b7ab-49ac-bc7b-5ecc01f7fc2b}

La date est stockée au format ISO8601 (yyyy-mm-dd).

Le type utilisé en base de donnée est `date`. 
Si l'attribut est dans un tableau, le type en base donnée sera `text`.

## Options {#core-ref:2bd18e1b-3547-4bcc-8ace-796676ac433e}

[options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496). 

Ce type d'attribut ne dispose d'aucune option spécifique.



<!-- links -->
[PHP_strftime]: http://php.net/manual/fr/function.strftime.php "documentation de strftime sur php.net"
[PHP_is_numeric]: php.net/manual/function.is-numeric.php "documentation sur php.net"
[CKEDITOR_home]: http://ckeditor.com/ "Site officiel de CKEditor"
[CKEDITOR_option]: http://docs.cksource.com/ckeditor_api/symbols/CKEDITOR.config.html "options de CKEDITOR"
[SORTTABLEJS_home]: http://www.kryogenix.org/code/browser/sorttable/ "site officiel de sorttable.js"
[JSCOLOR_home]: http://jscolor.com/ "site officiel de JSColor"
[JSCALENDAR_HOME]: http://www.dynarch.com/projects/calendar/old/ "site officiel de JSCalendar"
