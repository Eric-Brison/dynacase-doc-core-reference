# Action/Register

## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Enregistre une variable dans la session de l'utilisateur.

## Description longue

La variable est enregistrée dans la session "paramètre" (nom de session : "*freedom_param*") de l'utilisateur. Cette session est enregistrée sous forme de fichier dans le sous-répertoire `var/session` du répertoire d'installation Dynacase. L'identifiant de session est transmis par des cookies. Il est initialisé lors de la connexion.

### Signature

    [php]
    public function register(string $k, string $v) : bool|int

### Description


### Avertissements

Lors de l'enregistrement d'objet certaines valeurs comme par exemple les types *resource* ne pourront être enregistrés car elle ne peuvent être linéarisées. Pour plus de détails voir le fonctionnement des sessions sur le site PHP.

## Liste des paramêtres

k
: (string) [in] nom de la variable de session à enregistrer

v
: (mixed) [in] valeur à enregistrer en session. Il est possible d'enregistrer des objets.

## Valeur de retour

La méthode retourne un booléen pour indiquer si l'enregistrement a été effectué. Retourne *true* si l'enregistrement est fait sinon retourne *false*.

## Erreurs / Exceptions

La session n'est valide que lors d'un accès web. Les sessions ne sont pas utilisables en mode console et dans ce cas cette méthode retourne toujours *false*.

Si la clef est vide, la valeur retournée est *Session::SESSION_CT_ARG*


## Historique


## Exemples

    [php]
    function myAction(Action &$action) {
       $key=$action->getArgument('keyword');
       $action->register('myLastSearchKey',$key);
       $s=new SearchDoc($action->dbaccess,'MY_FAMILY');
       if ($key) {
         $s->addGeneralFilter($key);
       }
       $s->search();
    }

## Notes

La session est valide depuis la connexion de l'utilisateur. Elle est invalidée lorsque l'utilisateur se déconnecte explicitement depuis l'interface web en appuyant sur le bouton "Quitter". Plus généralement, la déconnexion est effectuée en appelant l'action AUTHENT:LOGOUT.
Elle est invalidée lorsque cette session n'a plus eu d'activité durant un certain temps. Ce temps est configurable avec les paramètres applicatifs "CORE_SESSIONTTL", "CORE_GUEST_SESSIONTTL" et "CORE_SESSIONMAXAGE".

## See also
 
Voir Action::read()
Voir Action::unRegister()