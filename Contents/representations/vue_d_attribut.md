# Vue d'attribut {#core-ref:26dca29e-92b3-445f-a6d8-51eaa297219a}

Les *vues d'attribut* permettent de définir la représentation d'un attribut.
Elles peuvent être utilisées lorsque la représentation par défaut du document
correspond, à l'exception de quelques attributs isolés. 

Les vues d'attributs sont déclarés avec les options :

*   `viewtemplate` : pour les vues de consultation
*   `edittemplate` : pour les vues de modification


Une vue d'attribut est composée de :

*   un fichier de template, définissant la structure,
*   une méthode (appelée contrôleur de vue) du document à représenter,
    définissant les valeurs.  
    Cette méthode peut également être omise. dans ce cas, dynacase fera appel
    au [contrôleur de vue par défaut][default_view_controleur].

Par convention :

*   le fichier de template porte l'extension xml,
*   son nom détermine le nom de la vue,
*   la méthode associée doit porter le même nom.  
    L'objet `Layout` est accessible au moyen de la propriété `lay` de l'objet
    courant (`$this->lay`).

## Le contrôleur de vue d'attribut {#core-ref:d1016f0b-2640-4756-8863-044ede03aaf0}

Pour qu'une méthode du document soit utilisable en tant que contrôleur d'une
vue, il est nécessaire de lui ajouter la phpDoc `@templateController` afin
de se prémunir d'une éventuelle exécution arbitraire de code.

les paramètres reçus par la méthode sont au nombre de 3 :

*   `$target` (string): nom de la fenêtre graphique qui sera utilisé pour les
    hyperliens (`"_self"` par défaut) ;
*   `$ulink` (booléen) : indique s'il faut générer les hyperliens (`true` par
    défaut) ;
*   `$abstract` (booléen) : indique s'il ne faut pas générer uniquement les
    attributs de la fiche résumé (`false` par défaut).

### Contrôleur d'attributs par défaut {#core-ref:9c6d90f7-84e8-4d84-bd75-69899b8d5b4f}

En l'absence de méthode correspondant à la vue, le contrôleur d'attributs par défaut est
appelé. Cette méthode dépend de l'option :

*   `viewtemplate` : en consultation, la méthode appelée est `Doc::viewDefaultCard`.
*   `edittemplate` : en modification, la méthode appelée est `Doc::viewProp` suivi de
    `Doc::editAttr`.

## Syntaxe d'une zone de vue d'attribut {#core-ref:a4458a39-3a5f-451d-8d6f-3a88244c5e03}

Une zone de vue d'attribut s'exprime sous la forme `APP:DOCVIEW:OPTIONS` :

**`APP`** (obligatoire)
:   Le nom de l'application dans laquelle se trouve le template.

**`DOCVIEW`** (obligatoire)
:   La nom du template et du contrôleur à utiliser.

`OPTIONS` (facultatif)
:   Une option de représentation. ces options dépendent du type de vue :
    
    *   [en édition][zone_options_view]
    *   [en modification][zone_options_edit]


Des paramètres supplémentaires peuvent être fournis en utilisant une syntaxe 
identique aux paramètres des URL. Les valeurs des paramètres doivent être 
encodés comme les URL (l'utilisation de `urlencode` est recommandé). La syntaxe complète est avec les paramètres : `APP:DOCVIEW:OPTIONS?param1=valeur1[&param=valeur]*`. 
Ces paramètres supplémentaires sont accessibles depuis le contrôleur avec la 
fonction `getHttpVars()`.

Le couple `APP:DOCVIEW` indique le template et le contrôleur à utiliser. Si
`DOCVIEW` ne comporte pas d'extension  l'extension `.xml` est ajouté dans le nom
du fichier template.  Le fichier template est recherché par la fonction
`getLayoutFile` dans le répertoire `APP/Layout`. Le fichier est d'abord
recherché avec le nom `DOCVIEW` tel qu'il  est décrit et s'il ne le trouve pas,
le nom en minuscule est recherché.

Le nom de la méthode est le nom `DOCVIEW`. Dans ce cas, la casse du nom de la
méthode  n'est pas prise en compte (comme pour les méthodes de PHP en général).

## Vue de consultation d'attribut {#core-ref:9cb7b313-7294-424d-bd86-a63155025902}

La vue d'attribut remplace la valeur d'un attribut

Elle s'insère à la place de la valeur d'un attribut depuis la zone `FDL:VIEWBODYCARD`.

Extrait d'une consultation de document avec la zone `FDL:VIEWBODYCARD` :

    [html]
    <table>
        <tr>
           <td>Label 1</td>
           <td>:</td>
           <td>valeur 1</td>
        </tr>
        <tr>
           <td>Label 2</td>
           <td>:</td>
           <td>valeur 2</td>
        </tr>
    </table>


Afin de spécifier la vue d'attribut à utiliser en consultation, il faut utiliser
l'option `viewtemplate`. Si l'attribut n°2 a une vue d'attribut le document de 
consultation sera :

    [html]
    <table>
        <tr>
           <td>Label 1</td>
           <td>:</td>
           <td>valeur 1</td>
        </tr>
        <tr>
           <td>Label 2</td>
           <td>:</td>
           <td>ICI LE RESULTAT DE LA VUE D'ATTRIBUT</td>
        </tr>
    </table>

La vue d'attribut sera présentée dans une cellule de tableau HTML comme
représenté ci-dessous.

|        |     |                                      |
| -----: | :-: | ------------------------------------ |
| Label1 |  :  | Valeur1                              |
| Label2 |  :  | ICI LE RESULTAT DE LA VUE D'ATTRIBUT |
|        |     |                                      |


Si l'option est portée sur un attribut
tableau (`array`) la vue remplacera tout le tableau.
Si l'option est portée sur un attribut
cadre (`frame`) la vue remplacera tout le contenu du cadre mais le contour avec 
le libellé sera conservé.


### Options des vues d'attribut en consultation {#core-ref:ffc29ae1-7438-4a5b-aca2-83dc98be4d9d}

Les options disponibles en consultation sont les suivantes :

`S`
:   signifie que le libellé de l'attribut ne sera pas affiché et le template
    prendra toute la largeur du document. Cette option n'est pas applicable si 
    l'attribut est de type `frame`.
    
    Dans ce cas le document de consultation sera :

    [html]
    <table>
         <tr>
           <td>Label 1</td>
           <td>:</td>
           <td>valeur 1</td>
        </tr>
        <tr>
           <td colspan="3">ICI LE RESULTAT DE LA VUE D'ATTRIBUT POUR L'ATTRIBUT N°2</td>
        </tr>
    </table>


La vue d'attribut avec l'option `S` sera présentée dans une cellule de
tableau HTML comme représenté ci-dessous :

<table style="width:auto">
         <tr>
           <td align="right">Label 1</td>
           <td>:</td>
           <td>valeur 1</td>
        </tr>
        <tr>
           <td  colspan="3">ICI LE RESULTAT DE LA VUE D'ATTRIBUT<br/>
            POUR L'ATTRIBUT N°2</td>
        </tr>
</table>

### Utilisation des valeurs du document en consultation {#core-ref:1a703a73-68a4-4f97-a422-7c5aa26d9822}

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

**Attention** : Toutes ces clés respectent les visibilités : si la visibilité 
d'un attribut est `H` pour un utilisateur, les clés `L_ATTRID` et `V_ATTRID` 
seront des chaînes vides. `S_ATTRID`, pour sa part, n'est pas affecté par les
visibilités.

Exemple d'un template d'attribut sans contrôleur :

    MYAPP/Layout/mySpecialText.html

    [html]
    <h2>
       La valeur de [L_MY_TEXT] est <strong>[V_MY_TEXT]</strong>
    </h2>

Dans cet exemple le template est associé à l'attribut `MY_TEXT` avec l'option 
`viewtemplate=MYAPP:mySpecialText.html`.

### Utilisation d'un contrôleur d'attribut spécifique

Le contrôleur d'attribut est identique à un contrôleur de
 [vue de documents][viewcontroler].

La seule différence c'est qu'il ne contrôle qu'un attribut ou un ensemble 
d'attribut dans le cas d'un tableau ou d'un cadre.

Exemple : 

    Method.MyFamily.php

    [php]
    /**
     * Affiche le nombre sur 3 chiffres
     * @templateController affichage en rouge si négatif, en vert sinon
     */
    public function mySpecialNumber($target = "_self", $ulink = true, $abstract = false)
    {
        $number=$this->getRawValue("my_number");
        if ($number > 0) {
            $this->lay->set("color", "green");
        } else {
            $this->lay->set("color", "red");
        }  
        $this->lay->set("theNumber", sprintf("%.03d",$number));
    }

    MYAPP/Layout/mySpecialNumber.html

    [html]
    <h2>  La valeur est   
        <strong style="color:[color]">[theNumber]</strong>
    </h2>

Dans cet exemple le template est associé à l'attribut `MY_NUMBER` avec l'option 
`viewtemplate=MYAPP:mySpecialNumber.html`. La méthode `mySpecialNumber()` 
est déclarée dans le fichier [_METHOD_][famprop] de la famille.


## Vue de modification d'attribut {#core-ref:4faa4b17-56fc-4e42-a091-f1a97b7591b8}

La vue d'attribut remplace le champ de saisie d'un attribut du formulaire

Elle s'insère à la place de la valeur d'un attribut depuis la zone 
`FDL:EDITBODYCARD`.

Extrait d'un formulaire de document avec la zone `FDL:EDITBODYCARD` :

    [html]
    <table>
        <tr>
           <td>Label 1 :</td>
           <td><input value="Value 1"/> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>
    <table>
        <tr>
           <td>Label 2</td>
           <td><input value="Value 2"> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>

Afin de spécifier la vue d'attribut à utiliser en modification, il faut utiliser
l'option `edittemplate`.

La vue d'attribut remplace le champ de saisie de l'attribut.

Si l'attribut n°2 a une vue d'attribut le formulaire de 
saisie sera :

    [html]
    <table>
        <tr>
           <td>Label 1 :</td>
           <td><input value="Value 1"/> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>
    <table>
        <tr>
           <td>Label 2</td>
           <td>ICI LE RESULTAT DE LA VUE D'ATTRIBUT </td>
        </tr>
    </table>

La vue d'attribut sera présentée dans une cellule de tableau HTML comme
représenté ci-dessous. Le template d'un champ doit retourner deux éléments : le
champ de saisie et les éventuelle boutons de contrôles séparé par des éléments
de cellule `</td><td>`. Car au final le tableau doit comporter trois colonnes pour 
avoir un alignement correct.

### Options des vues d'attribut en modification {#core-ref:54fc1da2-da41-4302-a4fa-bfebea1d640f}

Les options disponibles en modification sont les suivantes :

`S`
:   Signifie que le libellé de l'attribut ne sera pas affiché et le template
    prendra toute la largeur du document.
    
    L'insertion se fera dans le fragment html suivant :
&nbsp;

    [html]
    <table>
        <tr>
           <td>Label 1 :</td>
           <td><input value="Value 1"/> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>
    <table>
        <tr>
           <td colspan="3">ICI LE RÉSULTAT DE LA VUE D'ATTRIBUT </td>
        </tr>
    </table>

`U`
:   Signifie que l'input généré par le mot-clef `[V_ATTRNAME]` prendra toute la
    largeur disponible. Elle n'ajoute pas de `</td><td>` supplémentaire.
    Cette option est à utiliser si les mots-clefs `[V_ATTRNAME]` sont présents dans 
    le template. 
&nbsp;

    [html]
    <table>
        <tr>
           <td>Label 1 :</td>
           <td><input value="Value 1"/> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>
    <table>
        <tr>
           <td>Label 2 :</td>
           <td>RÉSULTAT DE LA VUE SANS AUTRE TD : Tableau à 2 cellules</td>
        </tr>
    </table>



### Utilisation des valeurs du document en modification {#core-ref:92002e19-2b6c-474c-9f6b-0ff265dce351}

le [contrôleur par défaut][default_view_controleur] fait automatiquement appel
aux méthodes `Doc::editAttr` et `Doc::viewProp`. Elles initialisent les clés
suivantes :


*   editAttr va créer :
    *   `L_ATTRID` pour chaque attribut : le libellé (traduit) de l'attribut,
         entouré d'une balise `<b/>` si l'attribut est obligatoire),
    *   `V_ATTRID` pour chaque attribut : un input pour l'attribut,
    *   `W_ATTRID` pour chaque attribut : `true` si l'attribut est visible, `false`
         sinon.
*   viewProp va créer :
    *   `ATTRID` pour chaque attribut : la valeur brute de l'attribut
    *   `PROPID` pour chaque propriété : la valeur brute de la propriété
    *   `V_TITLE` une ancre vers le document lui-même avec son titre

Lors de l'utilisation d'un contrôleur personnalisé, il est possible d'appeler
ces méthodes afin de générer les clés correspondantes. Il est également possible
de définir d'autres clés en utilisant les différentes méthodes du `Layout`.

Les clefs `V_ATTRID` fournies par `Doc::editattr()` retourne par défaut 
les 2 élements _champ de saisie_ et _boutons de contrôle_ séparés par 
`</td><td>` pour une insertion dans le formulaire.
La méthode `Doc::editAttr()` possède un argument qui permet d'omettre le 
séparateur `</td><td>` pour des constructions de vues plus spécialisées.

**Attention** : toutes ces clés respectent les visibilités : si l'utilisateur
n'a pas le droit de voir un attribut, la clé `V_ATTRID` génère un
`<input type="hidden"/>`.

Lors de l'utilisation d'un contrôleur personnalisé, il est possible d'appeler
ces méthodes afin de générer les clés correspondantes. Il est également possible
de définir d'autres clés en utilisant les différentes méthodes du `Layout`.


Exemple : 

    Method.MyFamily.php

    [php]
    /**
     * Affiche le nombre sur 3 chiffres
     * @templateController affichage en rouge si négatif, en vert sinon
     */
    public function myEditSpecialNumber($target = "_self", $ulink = true, $abstract = false)
    {
        $this->editAttr();
    }

    MYAPP/Layout/myEditSpecialNumber.html

    [html]
      Nombre à saisir
        [V_MY_NUMBER]
    
Dans ce cas le résultat sera 

    [html]
    <table>
        <tr>
           <td>Label 1 :</td>
           <td><input value="Value 1"/> ...</td>
           <td><input type="button"/> aide à la saisie/ extra link </td>
        </tr>
    </table>
    <table>
        <tr>
           <td>My number</td>
           <td>Nombre à saisir <input name=_"my_number" value="45"/></td><td></td>
        </tr>
    </table>

Ce qui donne la représentation suivante :

<table style="width:auto">
    <tr>
       <td style="vertical-align:middle;text-align:right">Label 1 :</td>
       <td><input value="Value 1"/> </td>
       <td><input type="button" value="..."/><input type="button" value="&times;"/>  </td>
    </tr>
    <tr>
       <td style="vertical-align:middle;text-align:right">My number</td>
       <td>Nombre à saisir <input name=_"my_number" value="45"/></td><td></td>
    </tr>
</table>

## Limitations {#core-ref:064493b3-7cc2-4cb8-9aa6-1ba96e11a228}

Les vues d'attribut ne sont pas gérées par Dynacase dans les vues de document
personnalisées. Elles sont utilisés que dans les vues `FDL:VIEWBODYCARD` pour la 
consultation et `FDL:EDITBODYCARD` pour la modification.

Chaque vue d'attribut utilise la même instance de l'objet `Doc`
correspondant au document en cours de consultation ou de modification.

Les vues d'attributs ne sont pas applicables aux attributs de type `tab`, ni 
aux attributs insérés dans un tableau. Dans ce dernier cas, il faut utiliser une 
[vue de tableau][array_row_view].

<!-- links --> 
[default_view_controleur]: #core-ref:9c6d90f7-84e8-4d84-bd75-69899b8d5b4f
[zone_options_view]: #core-ref:ffc29ae1-7438-4a5b-aca2-83dc98be4d9d 
[zone_options_edit]: #core-ref:54fc1da2-da41-4302-a4fa-bfebea1d640f 
[array_row_view]: #core-ref:9e76ac49-3b17-435b-ba25-a7122369be85 
[viewcontroler]: #core-ref:5da69221-eb2e-41a7-9f7a-d2c2e27c4184
[famprop]: #core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3
