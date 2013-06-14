# Écrire une action {#core-ref:e67d8aeb-939c-46e3-9be8-6fc3ba75ebc2}

Une action est le déroulement d'un code PHP et la production d'une sortie.
L'action peut être vue comme le traitement d'une requête particulière.

## Principe et spécification {#core-ref:1aebef95-6a01-4e46-a2b6-06e18f454bc3}

### Introduction {#core-ref:cdb5f957-d0e5-428f-b954-15f8782d4ce5}

Toutes les actions doivent être définies au sein d'une [application]
[application].
La description de l'action se fait dans le fichier [`MYAPP.app`][my_app.app]
dans la variable `$action_desc`.

Une action est définie à l'aide d'un fichier PHP et d'un template XML/HTML.
Le fichier PHP ou le template est optionnel, mais il faut au moins un des deux.
Chaque action peut définir son [droit d'accès (ACL)]
(#core-ref:a98b72ea-c063-4907-abc4-e5171ab55e59). 
Si l'utilisateur n'a pas le droit défini, l'exécution de l'action sera 
interdite. Si l'action n'a pas d'ACL, l'action sera considérée comme libre 
ainsi tout utilisateur aura le droit de l'exécuter.

Le nom du fichier PHP, du template et de la fonction, doivent être définis dans `MYAPP.app`. 

Exemple:
Pour la définition de `$app_desc` se reporter au chapitre [applications]
[my_app.app].

    Fichier MYAPP.app:

    [php]
    <?php
    $app_desc = array(...);// voir le chapitre sur les applications
    
    $action_desc = array(
        array(
          "name" => "MYACTION1",
          "short_name" => N_("action one"),
          "acl" => ...
          "root" => "Y" 
        ),
        array(
          "name" => "MYACTION2",
          "short_name" => N_("action two"),
          "acl" => ..
          "root" => "N",
          "script" => "myaction1.php",
          "function" => "mafonctionpouraction2",
          "layout" => "monlayoutpouraction2.xml"
        )
        );
    ?>

### Contenu possible pour `$action_desc` {#core-ref:90bf0711-7874-4c9d-bdf0-7d28becb7628}
**name** (obligatoire)
:   Indique le nom de référence de l'action.
    
    L'appel de l'action se fera en utilisant la valeur de ce paramètre.
    
    **attention** : Il ne doit pas dépasser 30 caractères.

**short_name** (obligatoire)
:   Description courte de l'action

**long_name** (facultatif)
:   Description longue de l'action.
    
    (s'il est omis le **long_name** est égal au **short_name**)

**script** (facultatif)
:   Nom du fichier PHP qui sera inclus lors de l'exécution de l'action.
    
    S'il est omis, le nom du script est le nom (**name**) de l'action en minuscules,
    suivi de l'extension `.php`
    
**function** (facultatif)
:   Nom de la fonction PHP qui sera appelée lors de l'exécution de l'action.
    Elle doit se trouver dans le fichier défini par **script**.
    
    S'il est omis, le nom de la fonction est le nom (**name**) de l'action en
    minuscules.

**layout** (facultatif)
:   Nom du fichier template utilisé lors de l'exécution de l'action.
    
    S'il est omis, le nom du template est le nom (**name**) de l'action en minuscules
    suivi de l'extension `.xml`

**available** (facultatif) 
:   Indique si l'action est disponible. Deux valeurs possibles : 
    
    *   `'Y'` : action disponible  (valeur par défaut)
    *   `'N'` : action non disponible.
    
    Une action indisponible ne peut plus être exécutée. Dans le cas d'une
    requête HTTP, le status _"503 Action unavalaible"_ sera renvoyé.

**acl** (facultatif)
:   Nom du droit nécessaire pour exécuter l'action.
    
    Le nom du droit doit être une des valeurs définies par la variable
    `$app_acl`. Une absence de valeur indique qu'il n'est pas nécessaire d'avoir
    un droit particulier pour exécuter l'action. Si un utilisateur tente
    d'exécuter une action dont il n'a pas les droits alors dans le cas d'une requête
    HTTP, le status _"503 Action forbidden"_ sera renvoyé.
    
    **Note** : l'utilisateur "admin" peut exécuter toutes les actions sans
    restriction de droits.

**root** (facultatif)
:   Indique que cette action est l'action principale de l'application. Deux 
valeurs possibles: 
    
    * 'Y' action principale. Dans ce cas l'action sera lancée avec l'url `?app=MYAPP`;
    * 'N' action non principale (valeur par défaut).
    
    Une seule action peut être notée "root". Dans le cas où plusieurs actions
    seraient notées "root", aucune erreur ne sera levée, mais, le résultat n'est
    pas garanti: l'action qui sera lancée sera la première "trouvée"


### Contenu d'un fichier exemple d'action: `myaction1.php` {#core-ref:47071800-7b9a-4ef1-b428-324ffa6293e9}

Le fichier `myaction1.php` contient une fonction du même nom que l'action avec 
comme paramètre une référence à l'objet [Action](#core-ref:29553eba-bcea-4baf-bef8-103c3a3510fa)


    Fichier myaction1.php

    [php]
    function myaction1(Action &$action) {
    // ...
    }

#### Récupérer des paramètres {#core-ref:a52dc8a3-8221-4496-8318-c565e9e657f4}
Pour récupérer 

* la valeur d'un [paramètre applicatif](#core-ref:c3d9cb18-16d0-435a-b8c2-5fa6ac06c522):

    [php]
    $parameterValue = $action->getParam("nom_du_paramètre");

* les coordonnées de la base de donnée:

    [php]
    $dbaccess = $action->dbaccess;

* l'utilisateur courant: 

    [php]
    $user = $action->user; // Objet de type `Account`

* l'application liée à l'action (retourne une instance d'objet de la classe [Application][classapplication]


    [php]
    $application = $action->parent // Objet de type `Application`

* les valeurs passées dans l'URL:

	Une action peut être lancée par l'activation d'un lien hypertexte. L'url appelée peut contenir des paramètres, dont les valeurs sont récupérées par l'intermédiaire de la méthode Action::getArgument

    [php]
    $val = $action->getArgument("url_val", "val_par_defaut");


#### Vérifier les arguments et donner l'usage {#core-ref:b9756f83-8a67-42fa-ad4d-0641ae3c886d}

La classe [ActionUsage][actionusage] permet de valider que les arguments reçus 
sont valides (attribut obligatoire/optionnel).

Si l'option strict est mise à `true` (valeur par défaut), tout argument non 
compris dans l'usage provoquera une erreur et l'action sera déroutée dès l'appel à `verify()`.

Exemple d'utilisation de `ActionUsage`:

    [php]
    function my_color(Action &$action)
    {
    	$usage = new ActionUsage($action);
        $usage->setText(_("Get color map"));
    	$red = $usage->addOptionalParameter("red", "red level", array(), 128);
    	$quality = $usage->addOptionalParameter("quality", "quality", array(), 20);
    	$usage->verify();
    	
    	if (!is_numeric($red)) $usage->exitError('red must be a integer');
    	if (!is_numeric($quality)) $usage->exitError('quality must be a integer');
    }


#### Afficher/Transmettre des données dans le template {#core-ref:3b806816-b4f3-415c-a22f-fe059b818d91}

Il faut utiliser l'attribut `lay` de l'objet `$action` qui est passé en
paramètre. L'attribut `lay` est un objet de la classe [`Layout`][class_layout] :

    [php]
    $action->lay->set("mydata", "val_to_be_sent");

Plus d'informations sur les template sont disponibles [ici][template]

#### Mise en garde et astuces {#core-ref:41079be9-2294-4bd6-ae76-cb6934a7302b}

* L'appel à  `$this->` ne fonctionne pas dans le fichier action : ce n'est pas un objet.
* Pour sortir de la fonction et afficher un message d'erreur à l'utilisateur,
 il faut utiliser la méthode [`exitError()`][exiterror] :

    [php]
    $action->exitError("Message d'erreur");


### Contenu d'un fichier exemple de template d'action: `myaction1.xml` {#core-ref:1daf83ca-fcb3-496f-8790-a1ce29c6bbf0}

Le template de l'action peut faire référence aux zones de l'application de FDL.
Pour cela, le contenu du fichier est inséré entre les 2 balises :

    [html]
    [ZONE FDL:HTMLHEAD]
    ...
    [mydata]
    [ZONE FDL:HTMLFOOT]

Cela rajoutera une entête et un pied de page au template qui incluront tous les 
fichiers nécessaires à l'affichage d'un template Dynacase.

La balise `HTMLHEAD` peut contenir un attribut `title` en plus:

    [html]
    [ZONE FDL:HTMLHEAD?title=mon titre]

Cela changera le titre de la page web en `mon titre`.

Le reste de la page entre les deux balises doit être du code HTML valide ou 
utiliser le [système de template de Dynacase](#core-ref:9073f5b0-3cde-4690-a7a2-ffb5c4c7b94f)

**Note** : Bien que la plupart des templates sont faits pour produire des pages 
HTML, le templat peut aussi produire tout type de données textuelles telles que
 du javascript, des css, du json ou du XML. Une action peut aussi retourner des 
 fichiers binaires telles que des images mais dans ce cas ce n'est pas l'objet 
 `lay` qui sera utilisé pour le retour.

## Exécuter une action {#core-ref:14b2cf06-da86-46be-832e-942e842c9552}

Une action est exécutée sur le serveur en indiquant le nom de l'application et
le nom de l'action dans l'url d'accès.

Le nom de l'application est indiqué dans le paramètre `app` et le nom de
l'action dans le paramètre `action`.

Exemple :

    ?app=MY_APP&action=MY_ACTION

Les actions peuvent aussi être exécutées en mode console avec [_wsh_][actionwsh].

<!-- links -->
[application]: #core-ref:395f44f1-6699-4ad8-b525-31e65e9b6efb
[my_app.app]: #core-ref:cf584c21-ebee-4444-8046-da3fa3a2db1b
[class_layout]: #core-ref:9f9edc1b-17a5-4f54-86ee-69e33016fe18
[exiterror]: #core-ref:D6845AA2-FACC-41B5-82D1-4681FCE55783
[actionusage]: #core-ref:7a8932eb-a59f-482a-9991-4ee1c634eae4
[classapplication]: #core-ref:5fca4352-702f-44fb-8ffa-3686545c6c67
[template]: #core-ref:af9ea76c-069e-49e1-a382-efc8ca35f1eb
[actionwsh] #core-ref:63832d9f-61a8-4846-a9d5-c34ee58de4a6