# Action/getParam
 

## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Cette méthode donne la valeur d'un paramètre applicatif

## Description longue

Cette méthode permet de récupérer la valeur d'un des paramètres de l'application dont est issu l'action. Les paramètres de l'application "*CORE*" et les paramètres globaux sont aussi disponibles. De plus cette méthode permet aussi de récupérer les valeurs des paramètres volatiles.

Si le paramètre choisi est un paramètre *utilisateur*, c'est la valeur choisie par l'utilisateur qui sera retournée. Si l'utilisateur n'a pas encore choisi de valeur pour ce paramètre c'est la valeur définie par le paramètre applicatif qui sera retourné.

Les paramètres volatiles généraux sont :
CORE_EXTERNURL
: Url d'accès au serveur. Elle est composé à partir du paramètre application "*CORE_URLINDEX*". Si ce paramètre n'est pas renseigné, il est composé en fonction de l'url d'accès à l'action.

ISIE
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer (toutes version confondues)

ISIE6
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 6

ISIE7
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 7

ISIE8
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 8

ISIE9
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 9

ISIE10
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 10

ISSAFARI
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Safari (Windows ou MacOs X)

ISCHROME
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Google Chrome (Windows , MacOs X ou Linux)

ISAPPLEWEBKIT
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Google Chrome ou Safari utilsant AppleWebKit.

### Signature

    [php]
    public function getParam($name, $def = "")

### Description


### Avertissements


## Liste des paramêtres

name
: [in] (string) nom du paramètre

def
: [in] (mixed) valeur retournée si la paramètre n'existe pas ou si la valeur du paramètre est strictement égal à *null*.

## Valeur de retour


## Erreurs / Exceptions


## Historique


## Exemples

    [php]
    // myaction.php - MY_PARAM est déclaré dans le fichier MYAPP_init.php
    function myAction(Action &$action) {

       if ($action->getParam("ISIE") {
         // Internet Explorer détecté
       }
       $myParam = $action->getParam("MY_PARAM");
    }

## Notes

Bien que cette méthode soit définie sur la classe Action, elle est un raccourci pour accéder à la méthode Application::getParam de l'application dont est issue l'action.

Les paramètres applicatifs sont déclarés dans le fichier &lt;APPLICATION_NAME&gt;_init.php.

Les valeurs des paramètres sont visibles et modifiable avec l'application *APPMNG*.

## See also

*  Voir Action::setVolatileParam()
*  Voir la classe *ParameterManager*
