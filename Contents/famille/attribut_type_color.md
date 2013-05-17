# Type `color` {#core-ref:4e42b385-fe99-41ac-8138-cbc8ef5076d6}

## Description {#core-ref:c041bd91-f095-41bf-b1dd-2d0dcb6ce806}

Les attributs de type *color* permettent d'insérer une couleur.

## Représentation {#core-ref:51a480cf-a90d-4092-ba66-1102b8c10ca5}

*   consultation :
    
    Un `span` contenant le code html de la couleur, et la couleur comme background.
    
    ![ color - consultation html ](famille/attributs/color-consultation.png "color - Consultation html")

*   modification :
    
    Un color picker basé sur [JSColor][JSCOLOR_home].
    
    ![ color - Modification html ](famille/attributs/color-modification.png "color - Modification html")

*   odt :
    
    Non utilisable

## Comportement {#core-ref:44695af9-ad45-40f1-8c1b-c14beade3c4f}

Aucun comportement particulier.

## Format de stockage {#core-ref:4ee50a19-5cee-438f-a505-d0d2978a4670}

La valeur stockée est le code html de la couleur.

Le type utilisé en base de donnée est `text`.

## Options {#core-ref:08390cd9-a465-4e7f-87e8-f4223295ada5}

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