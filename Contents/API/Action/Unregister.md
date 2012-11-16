# Action/Unregister
 

## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Supprime une variable de session utilisateur

## Description longue

La variable est supprimée de la session "paramètre" (nom de session : "*freedom_param*") de l'utilisateur.

### Signature

    [php]
    public function unRegister(string $k):bool

### Description


### Avertissements


## Liste des paramètres

k
: (string) [in] nom de la variable de session à supprimer

## Valeur de retour

Retourne toujours *true*.

## Erreurs / Exceptions


## Historique


## Exemples

    [php]
    function myAction(Action &$action) {
       $key=$action->getArgument('keyword');
       // suppression de la clef si la nouvelle clef contient moins de 3 caractères
       if (mb_strlen($key) < 3) $action->unRegister('myLastSearchKey');
       else $action->register('myLastSearchKey',$key);
       $s=new SearchDoc($action->dbaccess,'MY_FAMILY');
       if ($key) {
         $s->addGeneralFilter($key);
       }
       $s->search();
    }

## Notes


## See also

Voir Action::read()
Voir Action::register()
