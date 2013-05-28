# Principe d'une vue de document {#core-ref:cb3e2b97-ee6d-4cdf-aa25-b2e41d0d3156}
 
Les vues de documents permettent de définir la représentation d'un document.

Une vue de document est composée de :

*   un fichier de template, définissant la structure,
*   un contrôleur de vue permettant de remplir le template.
    Ce contrôleur est une méthode de la famille qui complète le template.
*   Un masque déterminant les visibilités (facultatif).



## Syntaxe d'une zone documentaire {#core-ref:49b96dc9-64e9-4f5a-a167-396282625c1e}


Pour référencer une zone documentaire, la syntaxe suivante est utilisée :
`APP:DOCVIEW:OPTIONS:TRANSFORMATION`, avec les correspondances suivantes :

**`APP`** (obligatoire)
:   Le nom de l'application dans laquelle se trouve le template.

**`DOCVIEW`** (obligatoire)
:   La nom du template et du contrôleur à utiliser.

`OPTIONS` (facultatif)
:   Une option de représentation. ces options dépendent du type de vue :
    
    *   [en édition][zone_options_view]
    *   [en modification][zone_options_edit]

`TRANSFORMATION` (facultatif)
:   Une transformation peut être appliquée après la composition de la vue. Cette
    transformation est effectuée par le [module de transformation][TE].
    
    Il suffit d'indiquer le nom du moteur à utiliser comme `pdf` pour une
    transformation en PDF. La transformation n'est possible' qu'avec l'option
    `B` (binary).


Des paramètres supplémentaires peuvent être fournis en utilisant une syntaxe
identique aux paramètres des URL. Les valeurs des paramètres doivent être
encodées comme les URL (l'utilisation de la [fonction `urlencode`]
[PHP_urlencode] est recommandée).  
La syntaxe complète avec les paramètres est donc :
`APP:DOCVIEW:OPTIONS:TRANSFORMATION?param1=valeur1[&param=valeur]*`.  
Ces paramètres supplémentaires sont accessibles depuis le contrôleur avec la
fonction dynacase `getHttpVars()`.

Le couple `APP:DOCVIEW` indique le template et le contrôleur à utiliser.

*   Le fichier template est recherché avec la logique suivante :
    1.  Si `DOCVIEW` ne comporte pas d'extension, alors l'extension `.xml` est
        ajoutée.
    1.  Le fichier template est recherché par la fonction `getLayoutFile` dans le
        répertoire `APP/Layout`.
        1.  Le fichier est d'abord recherché avec le nom `DOCVIEW` tel qu'il est
            décrit
        1.  Si le fichier n'est pas trouvé, le nom en minuscule est recherché.
*   Le nom de la méthode est le nom `DOCVIEW`.  
    Dans ce cas, la casse du nom de la méthode n'est pas prise en compte
    (comme pour les méthodes de PHP en général).

Exemples :

|    Identifiant de zone    |        Template valide         | Contrôleur valide |
| :------------------------ | :----------------------------- | :---------------- |
| `FDL:EDITBODYCARD`        | FDL/Layout/EDITBODYCARD.xml    | ::editbodycard()  |
|                           | FDL/Layout/editbodycard.xml    | ::editBodyCard()  |
| `FDL:VIEWBODYCARD:T`      | FDL/Layout/VIEWBODYCARD.xml    | ::viewBodyCard()  |
|                           | FDL/Layout/viewbodycard.xml    | ::viewbodycard()  |
| `MYAPP:myview.html`       | MYAPP/Layout/myview.html       | ::myView()        |
| `MYAPP:MYVIEW?extra=yes`  | MYAPP/Layout/MYVIEW.xml        | ::myview()        |
| `MYAPP:MYVIEW?extra=yes`  | MYAPP/Layout/mysimpleView.html | ::mySimpleView()  |
| `MYAPP:mySimpleview.html` | MYAPP/Layout/mysimpleview.html | ::mySimpleView()  |

## Définition de la vue de consultation {#core-ref:d59a0b84-49c8-470b-8f38-fb138eb62be5}

Lors de la consultation d'un document, Dynacase génère une page html complète.
Cette page est structurée comme suit :

    +-------------------------------------------------+
    | FDL:FDL_CARD                                    |
    |-------------------------------------------------|
    |                                                 |
    |  +-------------------------------------------+  |
    |  | FDL:VIEWCARD                              |  |
    |  |-------------------------------------------|  |
    |  |                                           |  |
    |  |  +-------------------------------------+  |  |
    |  |  | Vue de document (FDL:VIEWBODYCARD)  |  |  |
    |  |  |-------------------------------------|  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  +-------------------------------------+  |  |
    |  |                                           |  |
    |  +-------------------------------------------+  |
    |                                                 |
    +-------------------------------------------------+

Pour plus de précisions, se reporter à la liste des <span class="fixme" data-assignedto="MCO">Zones de référence</span>.

La vue de consultation par défaut est la zone `FDL:VIEWBODYCARD`. Elle utilise 
donc le template `FDL/Layout/viewbodycard.xml` et le contrôleur 
`Doc::viewbodycard()`.

L'url `?app=FDL&action=FDL_CARD&id=9` affiche le document avec sa vue par défaut.
Si la famille ne comporte pas de paramétrage spécifique de vue, cette url est 
équivalente à `?app=FDL&action=FDL_CARD&id=9&zone=FDL:VIEWBODYCARD`

### Options des vues documentaires en consultation {#core-ref:96d615e5-b6a6-46d3-b42d-4396dbc42b8b}

Les options disponibles en consultation sont les suivantes :

`V`
:   Pour les squelettes HTML, il signifie que le document sera affiché comme
    suit :
    
    *   inclusion des CSS systèmes dynacase
    *   pas de titre, pas d'icônes,
    *   affichage de la barre de menus
    
`T`
:   Pour les squelettes HTML, il signifie que le document sera affiché comme
    suit :
    
    *   inclusion des CSS systèmes dynacase
    *   pas de titre, pas d'icônes,
    *   pas de barre de menus

`U`
:   Pour les squelettes HTML, il signifie que le document sera affiché comme
    suit :
    
    *   pas d'inclusion des CSS systèmes dynacase
    *   pas de titre, pas d'icônes,
    *   pas de barre de menus

`S`
:   Signifie que la zone documentaire est autonome, qu'elle ne nécessite pas
    d'encapsulation HTML. Cette option est obligatoire pour tous les
    templates non HTML.  
    Lorsque cette option est utilisée avec un template html, la zone doit
    générer une page complète.

`B`
:   Pour les squelette non HTML binaires.
    Cas notamment des fichiers openDocumentText (`*.odt`).
    Dans ce cas le retour de la vue par la méthode `Doc::viewDoc()`
    sera le nom d'un fichier temporaire et non le contenu comme pour les zones
    textuelles.

## Définition de la vue de modification {#core-ref:bfbab9da-385a-45a3-af74-b17b4cca2e24}

Lors de la modification d'un document, Dynacase génère une page html complète.
Cette page est structurée comme suit :

    +-------------------------------------------------+
    | GENERIC:GENERIC_EDIT                            |
    |-------------------------------------------------|
    |                                                 |
    |  +-------------------------------------------+  |
    |  | FDL:EDITCARD                              |  |
    |  |-------------------------------------------|  |
    |  |                                           |  |
    |  |  +-------------------------------------+  |  |
    |  |  | Vue de document (FDL:EDITBODYCARD)  |  |  |
    |  |  |-------------------------------------|  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  |                                     |  |  |
    |  |  +-------------------------------------+  |  |
    |  |                                           |  |
    |  +-------------------------------------------+  |
    |                                                 |
    +-------------------------------------------------+

La vue de modification par défaut est la zone documentaire `FDL:EDITBODYCARD`.
Elle utilise donc le template `FDL/Layout/editbodycard.xml` et le contrôleur 
`Doc::editbodycard()`.

La vue de modification de document est toujours rendue encapsulée dans 
`FDL:EDITCARD`,elle-même rendue au sein de `GENERIC:GENERIC_EDIT`. Aussi 
cette vue retourne un fragment de formulaire, qui sera inséré dans 
le `form` de la page.

### Options des vues documentaires en modification {#core-ref:9e341064-ea78-4049-819c-8d0ab765840e}

Les options disponibles en modification sont les suivantes :

`S`
:   Le document est affiché comme suit :
    
    *   l'entête n'est pas affiché,
    *   les boutons *sauver* et *annuler* ne sont pas affichés.

`V`
:   Le document est affiché comme pour `S`
    
    (Obsolète) utilisé pour compatibilité version précédente.

`U`
:   Le squelette est affiché de manière brute et n'est pas encapsulé dans un
    formulaire.

`T`
:   Le document est affiché comme suit :
    
    *   l'entête n'est pas affiché,
    *   les boutons *sauver* et *annuler* sont affichés




<!-- links -->
[default_view_controleur]: #core-ref:1b7cb4c6-df1e-4124-8f5d-deaeac92561b
[CVDOC]: #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[TE]: #FIXME
[zone_options_view]: #core-ref:96d615e5-b6a6-46d3-b42d-4396dbc42b8b
[zone_options_edit]: #core-ref:9e341064-ea78-4049-819c-8d0ab765840e
[PHP_urlencode]: http://php.net/manual/fr/function.urlencode.php "fonction urlencode sur php.net"