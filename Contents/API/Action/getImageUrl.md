# Action/getImageUrl



## L'applicabilité

   Applicable

## Description courte

Cette méthode retourne l'url d'accès à une image stockée sur le serveur.

## Description longue

Si la détection de style n'est pas désactivé, l'image est recherchée dans le répertoire "*Images*" du répertoire du style *société* (nom provenant du paramètre application "*CORE_SOCSTYLE*"). Si l'image n'est pas présente, le répertoire du style utilisateur (paramètre applicatif "*STYLE*") est utilisé. De même, l'image est recherchée dans le sous-répertoire "*Images*" du repértoire de style.

Si l'image n'est pas redéfinie par un style, elle est recherchée dans le sous-répertoire "*Images*" du répertoire d'installation de l'application.

Si l'image n'est pas trouvée, elle est recherchée en dernier recourt dans le répertoire "*Images*" général du répertoire d'installation de Dynacase.



### Signature

    [php]
    public function getImageUrl(string $name, bool $detectstyle = true, int $size = null):string

### Description

-

### Avertissements

-

## Liste des paramètres


name
: [in] (string) nom du fichier image (*basename*).

detectstyle
: [in] (bool) indique si le style doit être pris en compte

size
: [in] (int) indique la largeur de l'image en pixel. Si la valeur n'est pas renseigné la taille originale est conservée sinon une conversion d'image sera appliquée afin d'avoir la largeur indiquée.

## Valeur de retour

L'url **relative** d'accès à l'image est retournée. Le résultat de cette fonction peut être mise dans le layout d'une action. Pour avoir une url absolue, il faut ajouter le paramètre "*CORE_EXTERNURL*" pour compléter l'url.

## Erreurs / Exceptions

Si l'image n'est pas trouvée, c'est l'image définie dans l'attribut "*noimage*" de la classe Application qui est retournée. Cette image est 'CORE/Images/noimage.png' :
![image non trouvée](images/noimage.png "No image")

## Historique


## Exemples

    [php]
    // myaction.php
    function myAction(Action &$action) {
       $imageUrl=$action->getImageUrl('myImage.png'); // image originale
       $smallImageUrl=$action->getImageUrl('myImage.png',true, 20); // 20 pixels de largeur
       // constitution d'une URL absolue
       $absoluteUrl=$action->getParam("CORE_EXTERNURL").$imageUrl;
    }


## Notes

Bien que cette méthode soit définie sur la classe Action, elle est un raccourci pour accéder à la méthode Application::getImageUrl de l'application dont est issu l'action.

## See also
