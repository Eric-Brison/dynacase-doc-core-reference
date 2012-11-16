# Action/Read


## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Récupère une variable dans la session de l'utilisateur.


## Description longue

Cette méthode permet de récupérer les valeurs de variables de sessions précédément enregistrées par la méthode `Action::register()`.

### Signature

    [php]
    public function Read(string $k, mixed $def = ""):mixed

### Description


### Avertissements


## Liste des paramètres

k
: (string) [in] nom de la variable de session à lire

def
: (mixed) [in] valeur retournée si la variable n'a pas été enregistrée précédemment


## Valeur de retour

La méthode retourne la valeur de la variable *k*.
Si la variable est non trouvé ou strictement égale à null, la valeur *def* est retourné.

## Erreurs / Exceptions

La session n'est valide que lors d'un accès web. Les sessions ne sont pas utilisables en mode console et dans ce cas cette méthode retourne toujours *def*.

## Historique


## Exemples

    [php]
    // myaction.php
    function myAction(Action &$action) {
        // Récupère le dernier mot recherché
       $myUserLastSearchKey=$action->read('myLastSearchKey');
       $s=new SearchDoc($action->dbaccess,'MY_FAMILY');
       if ($myUserLastSearchKey) {
         $s->addGeneralFilter($myUserLastSearchKey);
       }
       $s->search();
    }

## Notes


## See also

Voir Action::register()
Voir Action::unRegister()