# Type `enum` {#core-ref:625303d6-e5d1-40c3-b91d-d1b2e7307f67}

## Description {#core-ref:336860e2-0fb1-4351-b6e0-fac8e9f93822}

Les attributs de type *enum* permettent d'insérer des listes de choix, 
sous la forme *clé|libellé*.

## Représentation {#core-ref:47c0fb81-a866-4f13-8a4b-63b9d3287c74}

*   consultation :
    
    Le libellé, traduit le cas échéant.
    
    ![ enum - consultation html ](famille/attributs/enum-consultation.png "enum - Consultation html")

*   modification :
    
    Un input de type select présentant les libellés traduits le cas échéant.
    
    ![ enum - Modification html ](famille/attributs/enum-modification.png "enum - Modification html")

*   odt :
    
    Le libellé, traduit le cas échéant.
    
    ![ enum - consultation odt ](famille/attributs/enum-odt.png "enum - Consultation odt")

## Comportement {#core-ref:4999969e-7d5a-4140-b857-25d4cd2c0f22}

Aucun comportement particulier.

## Format de stockage {#core-ref:3ada8389-10b4-41da-a669-7a4c1845c165}

La valeur stockée est la clé.

Le type utilisé en base de donnée est `text`.

## Options {#core-ref:4f14142f-6aac-473f-a0e3-87803febb883}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

bmenu
:   Indique si l'énuméré doit apparaître en tant que filtre dans les interfaces de l'application *GENERIC*
    
    Les valeurs possibles sont :
    
    *   **`yes` (comportement par défaut)**
    *   `no`

boolcolor
:   Indique que l'énuméré sera représenté (en consultation) par un carré de couleur.
    
    Les valeurs possibles sont :
    
    *   Un couple de [couleurs css valides][MDN_css_color_value] séparées par une virgule (par exemple `blue,#FF0000`).
        La première couleur indique la couleur de la première clé, et la seconde couleur celle de la seconde clé.

eformat
:   Indique le mode d'affichage de l'énuméré.
    
    Les valeurs possibles sont :
    
    *   **`list` (comportement par défaut)**
        
        *   Dans le cas d'un énuméré simple, il sera représenté
            *   en modification sous la forme d'un select traditionnel,
            *   en consultation sous la forme d'une chaîne contenant le label
        
        *   Dans le cas d'un énuméré multiple, il sera représenté
            *   en modification sous la forme d'un select traditionnel (avec utilisation de la touche ctrl pour sélectionner plusieurs valeurs,
            *   en consultation sous la forme d'une liste de chaînes contenant le label alignées verticalement
    
    *   `vcheck`
        
        *   Dans le cas d'un énuméré simple, il sera représenté
            *   en modification sous la forme de boutons radio alignés verticalement
            *   en consultation sous la forme d'une chaîne contenant le label
        
        *   Dans le cas d'un énuméré multiple, il sera représenté
            *   en modification sous la forme de checkbox alignées verticalement
            *   en consultation sous la forme d'une liste de valeurs alignées verticalement
    
    *   `hcheck`
        
        *   Dans le cas d'un énuméré simple, il sera représenté
            *   en modification sous la forme de boutons radio alignés horizontalement
            *   en consultation sous la forme d'une chaîne contenant le label
        
        *   Dans le cas d'un énuméré multiple, il sera représenté
            *   en modification sous la forme de checkbox alignées horizontalement
            *   en consultation sous la forme d'une liste de valeurs alignées horizontalement
    
    *   `auto`
        
        la présentation de l'énuméré sera similaire à celle d'un attribut de type `docid`
    
    *   `bool`
        
        Ne s'applique qu'aux énumérés à 2 valeurs.
        
        L'énuméré sera présenté
        
        *   en modification sous la forme d'une checkbox (coché sélectionne la seconde valeur, non coché reste sur la première valeur)
        *   en consultation sous la forme d'une chaîne contenant le label

esort
:   Indique l'ordre dans lequel les entrées seront listées.
    
    Les valeurs possibles sont :
    
    *   **`none` (comportement par défaut)** Les énumérés sont présentés dans l'ordre de déclaration;
    *   `key` : Dans ce cas, les propositions sont triées par ordre alphabétique des clés ;
    *   `label` : Dans ce cas, les propositions sont triées par ordre alphabétique des traductions des libellés.

etype
:   Indique si la valeur est restreinte aux valeurs de la liste.
    
    Les valeurs possibles sont :
    
    *   `free` : Dans ce cas, l'utilisateur peut saisir une valeur libre
    *   `open` : Dans ce cas, l'utilisateur peut également saisir une valeur libre.
        Cette valeur sera alors ajoutée à la liste des valeurs possibles pour les choix ultérieurs.

eunset
:   Indiquer que l'énuméré sera vide par défaut.
    
    S'il y a une valeur par défaut explicite pour l'attribut, l'option eunset est inopérante.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (par défaut)** : Dans ce cas, la valeur par défaut est la première des valeurs de l'énuméré selon sa définition.

mselectsize
:   Indique le nombre d'items présentés pour les énumérés multiples lorsque 
    l'option eformat est `list`.
    
    Les valeurs possibles sont :
    
    *   tout entier.
    
    La valeur par défaut  est `3`.

multiple
:   Indique que l'énuméré peut être multivalué.
    
    **Les énumérés multiples ne peuvent pas être utilisés dans les tableaux**.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

system
:   Indique que la gestion de l'énuméré ne peut pas être faite par l'IHM d'administration.
    
    Dans ce cas, la définition est écrasée à chaque importation.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**



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