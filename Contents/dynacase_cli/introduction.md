# Dynacase en ligne de commande {#core-ref:1566c46d-a53d-44cf-8c3f-0d0e21c0b117}

L'exécution de programmes permettant de gérer les documents et le paramétrage en
général peut être fait en ligne de commande. Le point d'entrée de la ligne de
commande dans Dynacase est le script `wsh.php`.

## `wsh.php` {#core-ref:bab8c1c9-fe71-4629-9773-5cd67a8693bf}

Ce script permet de :

*   lancer des [scripts][wsh_script],
*   exécuter des [actions][wsh_action].

Son aide est disponible au moyen de l'option `--help` :

    ./wsh.php --help
    usage   wsh.php --app=APPLICATION --action=ACTION [--ARG=VAL] ...:  execute an action
            wsh.php --api=API [--ARG=VAL] ....   :  execute an api function
            wsh.php --listapi                     : view api list

### Utilisateur effectuant l'opération {#core-ref:f266fa37-8d4c-45f9-806f-154861bfc547}

Par défaut, les opérations sont lancées sous l'identité de l'utilisateur *Master
Default* (administrateur principal - compte `admin`). Il est possible de changer
cette identité au moyen de l'option `--userid`, qui prend comme paramètre le
*login* d'un utilisateur, ou son *identifiant système*.

### Passage d'arguments {#core-ref:fa9210eb-5bad-4867-a287-e732afc02251}

Il est possible de passer des arguments nommés en rajoutant des options avec la
notation `--argumentName=argumentValue`. Le nom de l'argument correspond au nom
de l'option. Ainsi, `--foo=bar` assignera la valeur `"bar"` à l'argument `foo`.

**Attention** : les arguments ne sont pas typés : ils sont systématiquement
envoyés au format texte. Aussi, lors de l'utilisation du paramètre `--foo=true`,
le script appelé recevra l'argument `"true"` (string) et non pas le booléen
`true`.

Si la valeur de l'argument comporte des espaces les double-quotes `"`ou les
quotes `'` peuvent être utilisées.

    ./wsh.php --api=my_test --my_number=3 --my_text="l'argument deux"

Pour la récupération des arguments, se référer à la documentation de la
[classe `ApiUsage`][ApiUsage].

Le passage d'arguments contenant plusieurs valeurs est faite en succédant le
nom de l'argument avec `[]`.

    ./wsh.php --api=my_test --my_numbers[]=2 --my_numbers[]=4

Dans ce cas la valeur de `my_numbers` sera :

    [php]
    array("2","4")


### Exécuter des scripts avec wsh {#core-ref:c47cdda0-0221-4dfc-ba14-56376e570372}

Exemple d'appel :

    ./wsh.php --api=dynacaseDbCleaner

Cela appellera le script `/API/dynacaseDbCleaner.php`.

La liste des scripts disponibles est obtenu au moyen de la commande *listapi* :

    ./wsh.php --listapi
    application list :
        - AppSwitcherSetCoreStartApp
        - DocRelInit
        - […]
        - vault_init
        - wdoc_graphviz

Afin de connaître l'usage d'un script, il est possible d'utiliser l'option
`--help` :

    ./wsh.php --api=dynacaseDbCleaner --help
    Clean base
    Usage :
        Options:
            --userid=<user system id or login name to execute function - default is (admin)>, default is '1'
            --real=<real (yes or no)>
            --help (Show usage)

### Exécuter des actions avec wsh {#core-ref:63832d9f-61a8-4846-a9d5-c34ee58de4a6}

Il est possible au moyen de *wsh* de lancer n'importe quelle action de n'importe
quelle application.

Exemple d'appel :

    ./wsh.php --app=MY_APP --action=MY_ACTION

Les arguments spécifiques de l'action doivent être indiqués au moyen de la
[syntaxe idoine][args]

Le résultat de l'action est retournée sur la sortie standard.

Exemple d'exécution de l'action `FDL_FAMILYSCHEMA` de l'application `FDL` :

    ./wsh.php --app=FDL --action=FDL_FAMILYSCHEMA --id=DIR > dir.xsd

### Retour d'erreur {#core-ref:982b9e0c-56ef-40c4-a8f8-0ae0826f07a2}

Le script retourne un *exit status* indiquant si une erreur s'est produite.
Lorsqu'une erreur se produit, son message est retourné sur la sortie standard
(*stdout*), et non sur la sortie d'erreur (*stderr*).

Codes retournés :

*   `0` : Pas d'erreur
*   `1` : Déclenchement d'une exception, appel à `Action::exitError()`, ou 
    action inconnue
*   `2` : Utilisateur inconnu ou non actif (option `--userid`)
*   `4` : Le script indiqué par `--api` est introuvable.

Exemple :

    $ ./wsh.php --api=pastrouve
    fichier API API/pastrouve.php non trouvé
    $ echo $?
    4

## Écrire un script CLI {#core-ref:4df1314f-9fdd-4a7f-af37-a18cc39f3505}

Les scripts exécutables avec wsh doivent être des fichiers php présents dans le
sous-répertoire `./API` du contexte d'installation. Ces fichiers doivent porter
l'extension `php` (le *basename* du fichier détermine le *nom de l'api*).

Lors du lancement d'un script, la variable `$action` est initialisée avec un
objet de la [classe `Action`][classe_action]. L'autoloader est initialisé, et
l'intégralité des fonctions et méthodes de Dynacase peuvent être utilisées sans
contrainte spécifique.

<!-- links -->
[wsh_script]: #core-ref:c47cdda0-0221-4dfc-ba14-56376e570372
[wsh_action]: #core-ref:63832d9f-61a8-4846-a9d5-c34ee58de4a6
[ApiUsage]: #core-ref:dac6d107-3e77-48ba-8912-ffccd0061cbf
[wsh_api]: #core-ref:c47cdda0-0221-4dfc-ba14-56376e570372
[classe_action]: #core-ref:29553eba-bcea-4baf-bef8-103c3a3510fa
[args]: #core-ref:fa9210eb-5bad-4867-a287-e732afc02251
