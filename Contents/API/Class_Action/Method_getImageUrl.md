# Action::getImageUrl() {#core-ref:4fc8d838-fee6-4e30-ada5-042cf6ab5903}

<div class="short-description">
Cette méthode retourne l'url d'accès à une image stockée sur le serveur.
</div>
<!--
<div class="applicability">
Applicable
</div>
-->

## Description {#core-ref:d2bc5661-d80e-45dd-80d4-9cea66c3e035}

    [php]
    string getImageUrl ( string $name [, bool $detectstyle = true [, int $size = null]] )

L'image demandée doit être une image fournie par l'application associée à l'action ou une autre application.

### Avertissements {#core-ref:0013302a-8251-4012-8174-fca6d9d30b10}

N/A

## Liste des paramètres {#core-ref:7b85d3c7-2c6c-489e-86df-ef682ab085ae}

(string) `name`
:   nom du fichier image (*basename*).

(bool) `detectstyle`
:   indique si la détection de style doit être pris en compte.
    
    valeur par défaut : **`true`**
   
    Si la détection de style est activée, l'image sera recherchée dans différents répertoires dans l'ordre suivant :
    
    1. L'image est recherchée dans le répertoire "*`Images`*" du répertoire du style *société* (nom provenant du paramètre application "*`CORE_SOCSTYLE`*"). 
    
    2. L'image est recherchée dans le répertoire du style utilisateur (paramètre applicatif "*`STYLE`*"). De même, l'image est recherchée dans le sous-répertoire "*`Images`*" du répertoire de style.
    
    3. L'image est recherchée dans le sous-répertoire "*`Images`*" du répertoire d'installation de l'application associée à l'action instanciée.
    
    4. Si l'image n'est pas trouvée, elle est recherchée en dernier recourt dans le répertoire "*`Images`*" général du répertoire d'installation de Dynacase. Ce répertoire contient des liens symboliques vers les images fournies par les applications installées.
    
    Si la détection de style n'est pas activée, les recherches n°1 et n°2 ne sont pas effectuées.

(int) `size`
:   indique la largeur de l'image en pixel. 
    
    valeur par défaut :  **`null`** indique qu'aucun redimensionnement ne sera effectué.
    
    Si la valeur n'est pas renseignée la taille originale est conservée sinon une conversion d'image sera appliquée afin d'avoir la largeur indiquée.
    Cette conversion d'image est effectuée sur le serveur lors du premier appel de l'url donnée. Ensuite le résultat de cette conversion d'image est mis en cache (répertoire `var/cache/images`) pour un accès plus rapide lors des prochains appels. Cette conversion retourne toujours une image au format *png*.

## Valeur de retour {#core-ref:ca0424a7-3135-4f23-830a-da1446203f52}

L'URL **relative** d'accès à l'image, par rapport à la racine du contexte, est retournée. Le résultat de cette fonction peut être mis dans le layout d'une action qui permet de référence des URL relatives. Pour avoir une url absolue, il faut ajouter le paramètre "*CORE_EXTERNURL*" pour compléter l'URL.

Si l'image n'est pas trouvée, c'est l'image définie dans l'attribut "*noimage*" de la classe Application qui est retournée. Cette image est 'CORE/Images/noimage.png' :
![image non trouvée](images/noimage.png "No image")

## Erreurs / Exceptions {#core-ref:b9b8aad9-6c82-4f2a-bf39-1a506f6c9f9a}

N/A

## Historique {#core-ref:dc8ab8a4-5a23-4ecc-a92e-8dc9cdd8cac7}

N/A

## Exemples {#core-ref:f6f2f704-3826-4b65-af1a-f423a8d5b623}

    [php]
    // myaction.php
    function myAction(Action &$action) {
      $imageUrl=$action->getImageUrl('myImage.png'); // image originale
      $smallImageUrl=$action->getImageUrl('myImage.png',true, 20); // 20 pixels de largeur
      // constitution d'une URL absolue
      $absoluteUrl=$action->getParam("CORE_EXTERNURL").$imageUrl;
    }

## Notes {#core-ref:2384b9ca-7fa8-469e-b04b-06e0ed0d8f56}

Bien que cette méthode soit définie sur la classe `Action`, elle est un raccourci pour accéder à la méthode `Application::getImageUrl()` de l'application dont est issu l'action.

## Voir aussi {#core-ref:edf5e295-3982-40bb-aa78-b3ce1a2fcf86}

N/A
