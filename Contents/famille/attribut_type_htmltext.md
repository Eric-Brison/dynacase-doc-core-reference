# Type `htmltext` {#core-ref:6ebf113a-1d6a-4c7a-be51-955955056bb3}

## Description {#core-ref:97b8259b-4df3-4450-99b0-c7d8fb5db785}

Les attributs de type *htmltext* permettent d'insérer du texte avec mise en forme.

Le langage de mise en forme est le html, et un éditeur WYSIWYG (basé sur [CKEditor][CKEDITOR_home]) permet d'en simplifier la saisie.

## Représentation {#core-ref:8f0bfff9-aaa6-4767-b905-d67a954e2ffa}

*   consultation :
    
    une `div` contenant la valeur.
    
    ![ htmltext - consultation html ](famille/attributs/htmltext-consultation.png "htmltext - Consultation html")

*   modification :
    
    une `iframe` dans laquelle est initialisé une instance de CKEditor.
    
    ![ htmltext - Modification html ](famille/attributs/htmltext-modification.png "htmltext - Modification html")

*   odt :
    
    la mise en forme est conservée.
    
    Se reporter au chapitre sur les vues odt
    pour les [restrictions][odt_restrictions] sur l'utilisation des attributs de
    type html dans les document openDocument text.

## Comportement {#core-ref:9bad041e-d747-4d9b-9406-5b62d662229b}

Lors de l'enregistrement, le nettoyage suivant est effectué :

*   Les balises `script` et `noscript` sont remplacées par des balises `pre` ;
*   Les entités UTF-8 sont décodées ;
*   Les commentaires sont supprimés.

## Format de stockage {#core-ref:083d2816-0682-4c35-b248-caa6e162b80e}

La valeur stockée est le html *nettoyé* selon les règles précédentes.

Le type utilisé en base de donnée est `text`. 

## Options {#core-ref:8e182116-8762-4157-a743-9abf43db0960}

En plus des [options communes à tous les types d'attributs](#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496), ce type d'attribut dispose des options suivantes :

doclink
:   Cette option nécessite l'installation du module dynacase-ckeditor-plugins.
    
    Active l'option doclink du HTMLEditor. Cette option se présente sous la forme d'un nouveau bouton (dans la partie réservée au lien dans les toolbar et en fin de toolbar sur la Basic), en cliquant sur le bouton une interface vous propose de sélectionner un document et ajoute une balise de lien vers ce document.
    
    Les valeurs possibles sont :
    
    *   un objet JSON (par exemple `{"famId": "DIR", "docrev" : "fixed"}`), contenant les propriétés suivantes :
        *   `famId` (obligatoire) : nom logique de la famille des documents cible,
        *   `docrev` (facultatif) : les valeurs possibles sont les mêmes que l'option *docrev* des attributs de type *docid* (latest, fixed, state(keystate)),
        *   `filter` (facultatif) : un filtre SQL qui sera appliqué à la recherche

editheight
:   Indique la hauteur de la zone d'édition.
    
    Les valeurs possibles sont :
    
    *   une taille en pixels (par exemple `400px`)
    
    La valeur par défaut est `150px`.

htmlclean
:   Indique que le serveur nettoiera le contenu en supprimant toutes les balises de style, généralement issues d'un copier/coller :
    
    *   les attribut des balises `span` et `font` sont supprimés ;
    *   les attributs `@class` et `@style` sont supprimés ;
    *   les balises `style` sont supprimés.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

jsonconf
:   Cette option permet de configurer finement l'éditeur de texte WYSIWYG.
    
    Elle permet notamment de fixer finement le comportement de l'éditeur et le contenu des toolbar.
    Les options de configuration sont [celles de CKEditor][CKEDITOR_option], et l'objet de configuration doit être présenté en JSON valide.
    
    Les options propres à CKEditor (*resize*, *correction orthographique*, etc) ne sont pas maintenues par Anakeen
    et leur bon fonctionnement n'est pas garanti par Anakeen.
    
    Aux options de CKEDITOR, dynacase ajoute les options suivantes :
    
    *   addPlugin : permet de charger un plugin additionnel.
        
        La valeur doit être un tableau (JSON) de noms logiques de plugins (par exemple: `"addPlugins": ["docattr"]`).
        Dans ce cas, le plugin doit posséder une commande ayant le même nom que le nom logique du plugin.
        Cette commande est alors ajoutée en fin de toolbar.
    
    Exemple de configuration permettant d'activer le plugin docattr et le plugin doclink et avec un menu basique et l'activation du mode resize :
    `jsonconf={"addPlugins" : ["docattr"], "doclink" :   {"famId" : "DIR"}, "toolbar" : "basic", "resize_enabled" : "true"}`
    
    **Attention** : l'utilisation de cette option bas niveau désactive les options suivantes :
    
    *   toolbar
    *   toolbarexpand
    *   editheight
    *   doclink
    
    Il est par contre possible de construire une option *jsonconf* qui a le même effet que les options précédentes.

toolbar
:   Indique le template à utiliser pour la barre de menu.
    
    Les valeurs possibles sont :
    
    *   **`Simple` (comportement par défaut)** :
        
        ![toolbar Simple](famille/attributs/htmltext-toolbar-simple.png)
    
    *   `Basic` :
        
        ![toolbar Basic](famille/attributs/htmltext-toolbar-basic.png)
    
    *   `Default` :
        
        ![toolbar Default](famille/attributs/htmltext-toolbar-default.png)
    
    *   `Full` :
        
        ![toolbar Full](famille/attributs/htmltext-toolbar-full.png)

toolbarexpand
:   Indique si la barre de menu doit être dépliée lors de l'affichage de l'éditeur.
    Dans le cas contraire, un petit bouton permet de la déplier.
    
    Les valeurs possibles sont :
    
    *   **`yes` (comportement par défaut)**
    *   `no`


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