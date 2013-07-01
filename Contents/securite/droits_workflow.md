# Paramétrage des droits pour un cycle de vie {#core-ref:e0d99925-df0d-4d51-8ebc-d44c4dd03873}

Le [cycle de vie][workflow] ne peut qu'avoir un profil dédié. Les droits d'un
workflow sont ceux d'un document auquel sont ajoutés un droit par type de
transition définie dans le cycle de vie.

## Transitions {#core-ref:7afaf95b-ff53-430e-aaf0-02992a551964}

Le profil du cycle de vie permet de donner les droits sur le passage de la
transition. Le nom du droit pour la transition est l'identifiant de la
transition utilisé dans [la propriété `$transitions`][wf_transitions] de la
[classe de cycle de vie][wf_class].

Extrait d'une classe de cycle de vie :

    [php]
    const TFirst = "my_firstTransition"; 
    const TSecond = "my_secondTransition"; 
    
    public $transitions = array(
        self::TFirst => array(),
        self::TSecond => array()
    );
    
    public $cycle = array(
        array(
            "e1" => "EA",
            "e2" => "EB",
            "t"  => self::TFirst
        ) ,
        array(
            "e1" => "EB",
            "e2" => "EC",
            "t"  => self::TSecond
        ) ,
        array(
            "e1" => "EA",
            "e2" => "EC",
            "t"  => self::TSecond
        )
    );

Dans ce cycle, deux droits `my_firstTransition` et `my_secondTransition` sont
ajoutés au profil de ce cycle.

Les cycles de vie ont la possibilité d'avoir un [profil dynamique][dynprof]
en indiquant la famille dans l'attribut "dynamique\famille" (`dpdoc_famid`).
Dans ce cas, ce sont les valeurs des attributs du document associé qui seront
utilisés pour vérifier les droits d'accès aux transitions.

Avec le profil suivant :

|     Compte    |        my_firstTransition       |       my_secondTransition       |
| ------------- | :-----------------------------: | :-----------------------------: |
| MY_FIRSTROLE  | <span class="aclgreen">X</span> |                                 |
| MY_SECONDROLE |                                 | <span class="aclgreen">X</span> |

les droits suivants sont obtenus sur les transitions :

| Rôles                         | Transition | Transition | Transition |
| ----------------------------- | :--------: | :--------: | :--------: |
| MY_FIRSTROLE                  | EA → EB    |            |            |
| MY_SECONDROLE                 |            | EB → EC    | EA → EC    |
| MY_FIRSTROLE et MY_SECONDROLE | EA → EB    | EB → EC    | EA → EC    |

Pour l'importation de droits sur un cycle de vie, les identifiants des
transitions sont utilisés pour référencer les droits spécifiques.

|            | Identifiant du profil |  /  | Option |              Droit              |               Droit               |
| ---------- | --------------------- | --- | ------ | ------------------------------- | --------------------------------- |
| __PROFIL__ | MY_WORKFLOW           |     | RESET  | my_firstTransition=MY_FIRSTROLE | my_secondTransition=MY_SECONDROLE |


## Profil d'étape {#core-ref:226eb791-83f5-4f6a-9ea1-bddc74cf9e73}

Pour chacune des étapes du cycle de vie, un profil peut être défini. Ce profil
sera associé au document attaché au cycle de vie lorsqu'il passera dans l'étape.
Ce profil lié doit être compatible avec le document associé.

Si aucun profil n'est attaché à une étape, le document conserve son profil
actuel lorsqu'il passe dans cette étape.




<!-- links -->
[workflow]:         #core-ref:55a53d99-0c24-48d8-8cb9-1caa171f2e9a
[dynprof]:          #core-ref:bc24834a-b380-4681-ae94-08b93076a7e8
[wf_transitions]:   #core-ref:0215aec3-671e-40b5-98e9-2ea651eff224
[wf_class]:         #core-ref:9da51559-24b0-4697-9620-a611a877a7e8