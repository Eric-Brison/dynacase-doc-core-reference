# Dcp\DocManager::getIdFromName() 

<div class="short-description">
Retourne l'identifiant associé au nom logique 
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static int Dcp\DocManager::getIdFromName ( string $documentName )


Retourne l'identifiant numérique associé au nom logique.

### Avertissements 

Aucun.

## Liste des paramètres 


(string) `documentName`
:   Nom logique du document


## Valeur de retour 

Retourne l'identitifiant de la dernière révision de document ayant le nom
logique indiqué.

## Erreurs / Exceptions 

Retourne `null` si le nom logique n'existe pas.

## Historique 

Remplace la fonction `getIdFromName`.

## Exemples 

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    $docId=\Dcp\DocumentManager::getIdFromName('MY_DOCUMENT');
    if ($docId !== null) {
        printf("Id %d", $docId);
    }

## Notes 

Aucun.

## Voir aussi 

*   `Dcp\DocManager::getNameFromId()`
