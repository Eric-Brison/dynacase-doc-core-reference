# Action/Set

## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Instancie l'objet à partir d'une action déclarée

## Description longue

Cette méthode permet d'initialiser l'objet afin de pouvoir utiliser l'action. Cette méthode est utilisée par le programme principal afin d'initialiser l'action demandée. L'action donnée en paramètre dans les fonctions de contrôle d'actions est déjà initialisé.
L'action à instancier doit indiquer l'application dont elle est issue.


### Signature

    [php]
    public function set(string $name, Application &$parent):void

### Description


### Avertissements


## Liste des paramêtres

name
: [in] (string) nom de l'action à instancier. Si le nom est vide, alors ce sera l'action principale (notée "*root*"=Y ) qui sera utilisée.

parent
: [in] (Application) L'objet *Application* déjà instancié dont est issu l'action. Ce paramètre est obligatoire.

## Valeur de retour

Aucun retour

## Erreurs / Exceptions

Si l'action n'existe pas dans l'application indiquée, une exception `\Dcp\Core\Exception` avec le code *CORE0005* est envoyé. De plus, dans ce cas, un header HTTP *503 Action unavalaible* est envoyé.

## Historique


## Exemples

Exemple complet d'une initialisation d'action. L'application de l'action utilise l'application "*CORE*" comme parent.

    [php]
    $core = new Application();
    // initialisation de l'application CORE
    $core->Set("CORE", $CoreNull=null);
    // initialisation de la session utilisateur
    $core->session = new Session();
    $core->session->set();
    $one = new Application();
    // initialisation de l'application ONEFAM en utilisant CORE en partageant la session
    $one->set("ONEFAM", $core, $core->session);
    $myAct=new Action();
    // initialisation de l'action ONEFAM_LIST en utilisant l'application ONEFAM
    $myAct->set("ONEFAM_LIST", $one);
    print $myAct->execute();

## Notes

L'application mis en paramètre doit avoir une session car celle-ci est partagée avec l'objet "Action". S'il n'y a pas de session, les méthodes Action::read(), Action::register() et Action::unRegister() ne seront pas fonctionnelles.

## See also
 
Voir Application::set()
