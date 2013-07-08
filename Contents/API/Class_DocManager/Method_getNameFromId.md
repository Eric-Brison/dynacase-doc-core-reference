# Dcp\DocManager::getNameFromId() 

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
    static string Dcp\DocManager::getNameFromId ( int $documentId )


Retourne le nom logique (propriété `name`) associé à l'identifiant numérique.

### Avertissements 

Aucun.

## Liste des paramètres 


(int) `documentId`
:   Identifiant numérique du document. Propriété (`id` ou `initid`).


## Valeur de retour 

Retourne le nom logique associé à l'identifiant numérique (propriété `id`).

## Erreurs / Exceptions 

Retourne `null` si l'identifiant n'existe pas.

## Historique 

Remplace la fonction `getNameFromId`.

## Exemples 

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    $docName=\Dcp\DocumentManager::getNameFromId(1234);
    if ($docName !== null) {
        printf("Nom logique : name = %s", $docName);
    }

## Notes 

Le même nom logique est associé à toutes les révisions d'un même document.

## Voir aussi 

*   `Dcp\DocManager::getIdFromName()`
