# Type `money` {#core-ref:2afb7c45-6108-4acc-9867-0c0a1723bcf9}

## Description {#core-ref:4203139d-c9a8-4cbc-a6cc-05d06d94593b}

Permet de représenter un format monétaire.

## Représentation {#core-ref:ecec88ee-96a4-4594-be7a-daf873d4620c}

*   consultation :
    
    Le nombre, formaté au moyen de la fonction [`money_format('%!.2n', …)`][PHP_money_format].
    
    ![ money - consultation html ](famille/attributs/money-consultation.png "money - Consultation html")
    
    Le formatage spécifique de *money* doit être conforme à celui utilisé dans la 
    fonction [sprintf][PHP_sprintf]. Par contre, il faut utiliser `%s` et non `%f` car le résultat donné à la fonction de formatage est ce qui est produit par *money_format*.
    Par exemple `money("%s €")` pour ajouter la devise de l'euro.

*   modification :
    
    un input de type texte permettant de saisir le nombre.
    
    ![ money - Modification html ](famille/attributs/money-modification.png "money - Modification html")

*   odt :
    
    Le nombre, formaté au moyen de la fonction [`money_format('%!.2n', )`][PHP_money_format].
    
    ![ money - consultation odt ](famille/attributs/money-odt.png "money - Consultation odt")

## Comportement {#core-ref:fe0e31bb-069b-4e47-9805-71b50fce7c75}

Lors de l'enregistrement, le nettoyage suivant est effectué :

*   remplacement des `,` par `.`
*   suppression des espaces

La valeur nettoyée est validée au moyen de la fonction [is_numeric][PHP_is_numeric].

## Format de stockage {#core-ref:0ab2dafa-5312-4d54-b160-dd7780664421}

La valeur stockée est la valeur nettoyée.

Le type utilisé en base de donnée est `double`. 

## Options {#core-ref:26c3a42c-1337-422f-8773-b677cef84699}

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