# La famille de Workflow {#core-ref:b8824399-f17d-4007-adde-8a7433939273}

La famille de workflow permet de spécifier :

*   le graphe du cycle ainsi que les attributs spécifiques au cycle,
*   les paramètres de familles qui seront utilisables lors des traitements
    spécifiques liés aux cycles.

## Définition de la famille {#core-ref:ccffad80-0c75-4fc1-9256-8acc5cf12c27}

Au même titre que les [autres familles][declaration_famille], une famille de
workflow est caractérisée par :

*   son code dans un fichier php
    
*   sa définition dans un fichier csv.
    
Cette famille doit :

*   Hériter de la famille `WDOC`

*   contenir les [propriétés][proprietes_famille] suivantes :
    *   `USEFOR;SW`.  
        Indique que la famille est
        *   Système (`S`),
        *   utilisable comme workflow (`W`).

*   être liée à une classe définissant les états et transitions du cycle.

### Exemple {#core-ref:be56f166-abe7-4f40-a1c2-7c0474c0fd5a}

|        |              |            |  |  |          |
| -      |              |            |  |  |          |
| BEGIN  | WDOC         | Cycle Demo |  |  | WFL_DEMO |
| USEFOR | SW           |            |  |  |          |
| CLASS  | Demo\WflDemo |            |  |  |          |
| END    |              |            |  |  |          |

## La classe de workflow {#core-ref:9da51559-24b0-4697-9620-a611a877a7e8}

La classe correspondante à un workflow doit définir la structure de ce workflow.
Cette structure s'exprime sous la forme d'un graphe, exprimé notamment au moyen
des propriétés de classe `$cycle` et `$transitions`.

### `$cycle` {#core-ref:d5ddda0c-09d2-42b0-9543-0723e242ec09}

La propriété `$cycle` définit le graphe à proprement parler. C'est un tableau à
2 dimensions ; chacun des sous-tableaux est de la forme

    [php]
    array(
        "e1" => "<état de départ>",
        "e2" => "<état d'arrivée>",
        "t"  => "<transition à utiliser>"
    );

où

*   `e1` est le libellé de l'état de départ,
*   `e2` est le libellé de l'état d'arrivée,
*   `t` est le nom de la transition à utiliser pour passer de l'état de départ à
    l'état d'arrivée.

### `$transitions` {#core-ref:0215aec3-671e-40b5-98e9-2ea651eff224}

La propriété `$transitions` définit l'ensemble des transitions utilisables.
C'est un tableau associatif à 2 dimensions ; la *clé* de chacun des sous-
tableaux correspond au *nom de la transition*, et chacun de ces sous-tableaux
est de la forme

    [php]
    array(
        "nr"  => true,
        "m0"  => "myFirstCondition",
        "m1"  => "mySecondCondtion",
        "m2"  => "myFirstProcess",
        "m3"  => "myLastProcess",
        "ask" => array("askId1", …)
    );

où

*   `nr` est un booléen indiquant qu'il ne faut pas demander de raison au
    changement d'état (*nr* pour *No Reason*).  
    La valeur par défaut est à `false` ; dans ce cas, une popup demande à
    l'utilisateur de préciser la raison du changement d'état.
*   `m0`, `m1`, `m2`, `m3` sont chacune le nom d'une méthode de la classe de
    workflow.
*   `ask` est un tableau d'identifiants de paramètres ou d'attributs du
    workflow, qui seront utilisés pour générer la demande des paramètres de
    transition.

### `$firstState` {#core-ref:41a4297b-4623-4dc0-8a75-4d69d3e9ff0a}

La propriété `$firstState` définit l'état initial des documents liés à ce cycle
de vie. Elle désigne le libellé d'un état.

### `$attrPrefix` {#core-ref:2fb83350-741c-4936-9ae4-34b9f481d098}

Lors de la génération d'un cycle de vie, Dynacase génère un grand nombre
d'attributs pour paramétrer finement chaque état et chaque transition. ces
attributs sont préfixés par `$attrPrefix` pour éviter les éventuelles collisions
en base de données.

### `$stateActivity` {#core-ref:e75c4b8d-ec3c-4be9-8824-5ef5fe4117a3}

La propriété `$stateActivity` définit l'ensemble des activités. C'est un tableau
associatif ; la clé est le libellé de l'état et la valeur et le libellé de
l'activité.

### exemple {#core-ref:39cce5a0-2fae-461b-99e8-fbe91f67a172}

Considérons le [workflow de l'introduction][wf_intro]. La classe le définissant
contiendra :

    [php]
    
    namespace Demo;
    
    Class WflDemo extends \dcp\family\WDoc
    {
        public $attrPrefix = "DEMO";
        public $firstState = self::etat_created;
        public $viewlist = "none";
        
        //region States
        const etat_created    = "myapp_demo_e1";
        const etat_redacted   = "myapp_demo_e2";
        const etat_verified   = "myapp_demo_e3";
        const etat_diffused   = "myapp_demo_e4";
        const etat_archived   = "myapp_demo_e5";
        const etat_abandonned = "myapp_demo_e6";
        //endregion
        
        //region Transitions
        const transition_created_redacted    = "myapp_demo_t1";
        const transition_redacted_created    = "myapp_demo_t2";
        const transition_redacted_verified   = "myapp_demo_t3";
        const transition_verified_created    = "myapp_demo_t4";
        const transition_verified_diffused   = "myapp_demo_t5";
        const transition_diffused_archived   = "myapp_demo_t6";
        const transition_created_abandonned  = "myapp_demo_t7";
        const transition_redacted_abandonned = "myapp_demo_t8";
        const transition_verified_abandonned = "myapp_demo_t9";
        //endregion
        
        public $stateactivity = array(
            self::etat_created    => "demo:activity:etat_created",
            self::etat_redacted   => "demo:activity:etat_redacted",
            self::etat_verified   => "demo:activity:etat_verified",
            self::etat_diffused   => "demo:activity:etat_diffused",
            self::etat_archived   => "demo:activity:etat_archived",
            self::etat_abandonned => "demo:activity:etat_abandonned"
        );
        
        public $transitions = array(
            self::transition_created_redacted    =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_redacted_created    =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_redacted_verified   =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_verified_created    =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_verified_diffused   =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_diffused_archived   =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_created_abandonned  =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_redacted_abandonned =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            ),
            self::transition_verified_abandonned =>array(
                "m0" => "",
                "m1" => "",
                "m2" => "",
                "m3" => "",
                "nr" => true
            )
        );
        
        public $cycle = array(
            
            array(
                "e1" => self::etat_created,
                "e2" => self::etat_redacted,
                "t"  => self::transition_created_redacted
            ),
            array(
                "e1" => self::etat_redacted,
                "e2" => self::etat_created,
                "t"  => self::transition_redacted_created
            ),
            array(
                "e1" => self::etat_redacted,
                "e2" => self::etat_verified,
                "t"  => self::transition_redacted_verified
            ),
            array(
                "e1" => self::etat_verified,
                "e2" => self::etat_created,
                "t"  => self::transition_verified_created
            ),
            array(
                "e1" => self::etat_verified,
                "e2" => self::etat_diffused,
                "t"  => self::transition_verified_diffused
            ),
            array(
                "e1" => self::etat_diffused,
                "e2" => self::etat_archived,
                "t"  => self::transition_diffused_archived
            ),
            array(
                "e1" => self::etat_created,
                "e2" => self::etat_abandonned,
                "t"  => self::transition_created_abandonned
            ),
            array(
                "e1" => self::etat_redacted,
                "e2" => self::etat_abandonned,
                "t"  => self::transition_redacted_abandonned
            ),
            array(
                "e1" => self::etat_verified,
                "e2" => self::etat_abandonned,
                "t"  => self::transition_verified_abandonned
            )
        );
    }

Quelques remarques sur ce code :

*   Toutes les activités et tous les états ont été définis au moyen de
    constantes.
    
    Cela n'est en aucun cas obligatoire, mais permet d'éviter les erreurs de
    copier-coller ; en effet, les libellés des états, ainsi que les noms des
    transitions sont utilisés à de nombreux endroits.
    
*   Les noms des états et des transitions ont été *anonymisés*, et seules les
    constantes ont des labels intelligibles.
    
    Puisque les états et transitions vont générer des attributs, ils vont
    également générer des colonnes en base de données. Ces colonnes sont nommées
    à partir du nom de l'état ou de la transition. Aussi, si demain le client
    décide que l'état *archivé* doit devenir *classé*, il faudra soit accepter
    que le nom affiché et le nom stocké soient différents, soit renommer des
    colonnes en base de données et mettre à jour des fichiers de paramétrage.
    Aucun de ces 2 choix n'est pérenne ou dénué de risque.
    
    Avec des constantes anonymisées, il n'y a rien à changer en base de données,
    ni dans les fichiers de paramétrage, il suffit de changer la traduction de
    ce libellé. Accessoirement, on peut renommer la constante en bénéficiant de
    l'assistance d'outils de *refactoring*.

## Internationalisation {#core-ref:4c1b28c1-53bb-48c8-a8a6-8c809cd8dfef}

Dans un workflow, les éléments qui peuvent internationalisés sont :

*   le nom des états
*   le nom des activités
*   le nom des transitions

Pour être internationalisés, ces éléments doivent être ajoutés aux [catalogues
de traduction][translation_catalog].

<!-- links -->
[declaration_famille]: #core-ref:4b4cb93e-e717-4a42-888d-c2376deab4bb
[family_properties]: #core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3
[family_parameters]: #core-ref:4595c8e7-5002-4dbc-b6bb-882b4123efd8
[wf_intro]: #core-ref:55a53d99-0c24-48d8-8cb9-1caa171f2e9a
[internationalisation]: #core-ref:8f3ad20a-4630-4e86-937b-da3fa26ba423
[translation_catalog]: #core-ref:ca73ff9e-ceb8-456b-bdd4-9b9056f1543d