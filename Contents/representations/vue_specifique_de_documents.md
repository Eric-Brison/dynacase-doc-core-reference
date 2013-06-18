# Vue spécifique de document {#core-ref:2e11bee8-ff4b-46be-b5c1-77972db7c2f9}

La définition d'une nouvelle vue de document nécessite un _contrôleur de vue_ et
un _template_.

Le contrôleur de vue peut être omis. dans ce cas, Dynacase fera appel
 au [contrôleur de vue par défaut][default_view_controleur].

## Le contrôleur de vue {#core-ref:5da69221-eb2e-41a7-9f7a-d2c2e27c4184}

Pour qu'une méthode du document soit utilisable en tant que contrôleur d'une
vue, il est nécessaire de lui ajouter la phpDoc `@templateController` afin
de se prémunir d'une éventuelle exécution arbitraire de code.

les paramètres reçus par la méthode sont au nombre de 3 :

*   `$target` (string): nom de la fenêtre graphique qui sera utilisé pour les
    hyperliens (`"_self"` par défaut) ;
*   `$ulink` (booléen) : indique s'il faut générer les hyperliens (`true` par
    défaut) ;
*   `$abstract` (booléen) : indique s'il faut générer uniquement les
    attributs de la fiche résumé (`false` par défaut).

Par convention :

*   le fichier de template porte l'extension xml,
*   son nom (en minuscule) détermine le nom de la vue,
*   la méthode associée doit porter le même nom (la casse du nom de la méthode
    n'est pas prise en compte).  
    L'objet `Layout` est accessible au moyen de la propriété `lay` de l'objet
    courant (`$this->lay`).

Par exemple, considérons la méthode `mySpecialView` :

    [php]
    /**
     * default view for a family
     * @templateController special view
     * @return void
     */
    function mySpecialView($target = "_self", $ulink = true, $abstract = false)
    {
        $this->viewdefaultcard($target, $ulink, $abstract);
        
        $myItems = $this->getMultipleRawValues("my_items");
        $items = array();
        foreach ($myItems as $cle => $val) {
            $items[] = array(
                "itemValue" => $val
            );
        }
        
        $this->lay->setBlockData("ITEMS", $items);
    }

Le template associé peut être :

    MYAPP/Layout/myspecialview.xml

    [html]
    <ol>[TEXT:myapp:List of items]
    [BLOCK ITEMS]<li>[itemValue]</li>[ENDBLOCK ITEMS]
    </ol>

## Vue spécifique de consultation {#core-ref:284b75f4-7b2c-40ff-9ec8-122e526e5857}

La vue spécifique d'un document doit retourner un fragment HTML qui sera inclus
dans le corps de la page HTML.

La vue personnalisée est toujours rendue encapsulée dans `FDL:VIEWCARD`, elle-
même rendue au sein de `FDL:FDL_CARD`(sauf si l'[option][zone_options_view] `S`
est utilisée) . Aussi cette vue personnalisée doit générer un fragment qui sera
inséré dans le `body` de la page HTML.

    +-------------------------------------------------+
    | FDL:FDL_CARD                                    |
    |-------------------------------------------------|
    |                                                 |
    |  <body>...                                      |
    |                                                 |
    |  +-------------------------------------------+  |
    |  | FDL:VIEWCARD                              |  |
    |  |-------------------------------------------|  |
    |  |                                           |  |
    |  |  <div>                                    |  |
    |  |                                           |  |
    |  |  +-------------------------------------+  |  |
    |  |  | Vue spécifique de document          |  |  |
    |  |  |-------------------------------------|  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  +-------------------------------------+  |  |
    |  |                                           |  |
    |  |  </div>                                   |  |
    |  |                                           |  |
    |  +-------------------------------------------+  |
    |                                                 |
    |  </body>                                        |
    |                                                 |
    +-------------------------------------------------+


Afin de définir une vue personnalisée, il est possible :

*   d'utiliser un [contrôle de vue][CVDOC],
*   de spécifier une zone en paramètre http : pour ce faire, il suffit de passer
    l'identifiant de la zone documentaire dans le paramètre `zone` de l'url
    d'accès au document.
*   d'indiquer la zone documentaire dans l'attribut `defaultView` du fichier
   _CLASS_  de la famille pour avoir cette vue par défaut lors de la
    consultation.

    [php]
    public $defaultView='MYAPP:MYSPECIALVIEW'

### Contrôleur par défaut {#core-ref:1b7cb4c6-df1e-4124-8f5d-deaeac92561b}

#### Définition du contrôleur par défaut {#core-ref:97e54010-0310-4516-bccb-4d38671963e7}

En l'absence de méthode correspondant à la vue, le contrôleur par défaut
`Doc::viewDefaultCard` est appelé. 

Ce contrôleur est fait pour les vues de consultations et n'est pas adapté pour
les vues de modification.

#### Utilisation des valeurs du document {#core-ref:a5c38657-4537-404f-b908-c2684d343880}

Le [contrôleur par défaut][default_view_controleur] fait automatiquement appel
aux méthodes `Doc::viewAttr` et `Doc::viewProp`. Elles initialisent les clés
suivantes :

*   viewAttr va créer :
    *   `L_ATTRID` pour chaque attribut : le libellé (traduit) de l'attribut,
    *   `V_ATTRID` pour chaque attribut : la valeur (au format html) de
        l'attribut,
    *   `S_ATTRID` pour chaque attribut : `true` si l'attribut est vide, `false`
        sinon
*   viewProp va créer :
    *   `ATTRID` pour chaque attribut : la valeur brute de l'attribut
    *   `PROPID` pour chaque propriété : la valeur brute de la propriété
    *   `V_TITLE` une ancre vers le document lui-même avec son titre

**Note** : Toutes ces clefs sont en majuscules.

Lors de l'utilisation d'un contrôleur personnalisé, il est possible d'appeler
ces méthodes afin de générer les clés correspondantes. Il est également possible
de définir d'autres clés en utilisant les différentes méthodes du `Layout`.

**Attention** : toutes ces clés respectent les visibilités : si la visibilité 
d'un attribut est `H` pour un utilisateur, les clés `L_ATTRID` et `V_ATTRID` 
seront des chaînes vides. `S_ATTRID`, pour sa part, n'est pas affecté par les
visibilités.

Exemple d'un template sans contrôleur :

    MYAPP/Layout/mysimpleview.xml

    [html]
    <h1>[V_TITLE]</h1>
    
    <p>L'attribut [L_MY_TEXT] a la valeur : <strong>[V_MY_TEXT]</strong></p>

Dans cet exemple l'attribut `MY_TEXT` fait partie de la définition du document.

## Vue spécifique de modification {#core-ref:b2da68cb-2441-4f17-896f-ecffde9aae32}

Le template d'une vue de modification s'insère dans un formulaire HTML.
Il est composé de champs de formulaire afin de permettre à l'utilisateur
d'effectuer la saisie.

Il est aussi possible d'ajouter des `css` et des `js` spécifique
(Se reporter au chapitre [Moteur de template][advancedtemplate]).

    +-------------------------------------------------+
    | GENERIC:GENERIC_EDIT                            |
    |-------------------------------------------------|
    |                                                 |
    |  <body>                                         |
    |                                                 |
    |  +-------------------------------------------+  |
    |  | FDL:EDITCARD                              |  |
    |  |-------------------------------------------|  |
    |  |                                           |  |
    |  |  <form>                                   |  |
    |  |                                           |  |
    |  |  +-------------------------------------+  |  |
    |  |  | Vue spécifique de formulaire        |  |  |
    |  |  |-------------------------------------|  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  +-------------------------------------+  |  |
    |  |                                           |  |
    |  |  </form>                                  |  |
    |  |                                           |  |
    |  +-------------------------------------------+  |
    |                                                 |
    |  </body>                                        |
    |                                                 |
    +-------------------------------------------------+

### Utilisation des champs de formulaire du document {#core-ref:37dd7910-1c29-461f-9628-5f50c543ed2d}

Pour les vues de modifications de documents le contrôleur par défaut n'est pas
adapté car il ne fournit que des valeurs d'attributs et non des champs de saisie
pour un formulaire.

Pour avoir l'équivalent du contrôleur par défaut en modification il faut 
utiliser la méthode `Doc::editAttr`. Cette méthode initialise les clés
suivantes :

*   `L_ATTRID` pour chaque attribut : le libellé (traduit) de l'attribut,
    (entouré d'une balise `<b/>` si l'attribut est obligatoire),
*   `V_ATTRID` pour chaque attribut : un input pour l'attribut,
*   `W_ATTRID` pour chaque attribut : `true` si l'attribut est visible, `false`
    sinon.

**Note** : Toutes ces clefs sont en majuscules.

**Attention** : toutes ces clés respectent les visibilités : si l'attribut a 
une visibilité `H` (caché) pour l'utilisateur, la clé `V_ATTRID` génère un
`<input value="the value" type="hidden"/>`. Si la visibilité est `I` (invisible)
aucun champ n'est retourné. Les clés `L_ATTRID` ne sont pas affectées par la
visibilité.

Lors de l'utilisation d'un contrôleur personnalisé, il est possible d'appeler
ces méthodes afin de générer les clés correspondantes. Il est également possible
de définir d'autres clés en utilisant les différentes méthodes du `Layout`.

### Utilisation d'un contrôleur spécifique de modification {#core-ref:1f1191ea-a02b-4a28-a26b-81a43a7f7d29}

Le contrôleur de modification n'est applicable qu'au formulaire HTML. 

    [php]
    /**
     * default edit for a family
     * @templateController special edit
     * @return void
     */
    function mySpecialEdit($target = "_self", $ulink = true, $abstract = false)
    {
        $this->lay->set("textValue", $this->getRawValue("my_text"));
        $textAttribute=$this->getAttribute("my_text");
        $this->lay->set("textLabel", $textAttribute->getLabel());
    }

Le template associé peut être :

    MYAPP/Layout/myspecialedit.xml

    [html]
    <h1>Modifier la valeur de [textLabel]</h1>
    
    <input name="_my_text" value="[textValue]"/>
    

Le nom (attribut `name`) des champs de formulaire doit être précédé de `_`
(underscore) pour être pris en compte lors de la soumission de façon automatique.
Sinon, il est possible de récupérer tout autre champ dans le hook `preStore` 
avec la fonction `getHttpVars()`.

<!-- links -->
[default_view_controleur]: #core-ref:1b7cb4c6-df1e-4124-8f5d-deaeac92561b
[CVDOC]: #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[TE]: #FIXME
[advancedtemplate]: #core-ref:af9ea76c-069e-49e1-a382-efc8ca35f1eb
[zone_options_view]: #core-ref:96d615e5-b6a6-46d3-b42d-4396dbc42b8b
[zone_options_edit]: #core-ref:9e341064-ea78-4049-819c-8d0ab765840e