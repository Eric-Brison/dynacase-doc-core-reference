# Action/getArgument



## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Cette méthode permet de récupérer la valeur d'un argument donné dans le cadre d'une exécution d'action.

## Description longue

Cette méthode peut être utilisée dans le cadre de l'exécution d'une action ou dans un script *wsh*.
Dans le cas d'une action exécutée depuis une interface web, elle récupère les valeurs des arguments dans les variables HTTP. Dans le cas d'une action exécutée avec *wsh*, les arguments sont issus de la ligne de commande.

### Signature

    [php]
    public static function getArgument($k, $def = '')

### Description

-

### Avertissements


## Liste des paramêtres

k
: [in] (string) nom du paramètre

def
: [in] (mixed) valeur à retourner si le paramètre n'est pas renseigné

## Valeur de retour

La valeur retournée est la valeur du paramètre. Dans le cas où le paramètre n'est pas indiqué c'est la valeur de "def" qui est retourné.

| Paramètre url | Appel                 | Retour        |
|---------------|-----------------------|---------------|
|  &x=2&y=3     | getArgument('x')      |   2           |
|  &x=2&y=3     | getArgument('x', 5)   |   2           |
|  &x=2&y=3     | getArgument('z')      |   ''          |
|  &x=2&y=3     | getArgument('z',null) |   null        |
|  &x=2&y=      | getArgument('y',4)    |   ''          |


## Erreurs / Exceptions

Aucunes

## Historique

-

## Exemples

Exemple de la fonction d'une action :
>    exemple d'url d'accès à l'action : ` ?app=MY_APP&action=MY_ACTION&my_identifier=45`

    [php]
    // myaction.php
    function myAction(Action &$action) {
       $identifier=$action->getArgument("my_identifier");
       if (empty($identifier)) {
            $action->exitError("Need identifier");
       }
       $option=$action->getArgument("my_option","testing");
       if ($option=="testing") {
           // default setting
       }
    }


Exemple d'un script wsh
>    exemple de commande `./wsh.php --app=MY_APPLICATION --action=MY_ACTION --my_identifier=45`

    [php]
    $identifier=$action->getArgument("my_identifier"); // ici l'accès à l'action est directement accessible via la variable $action

## Notes


## See also

Voir aussi la classe "*ActionUsage*".