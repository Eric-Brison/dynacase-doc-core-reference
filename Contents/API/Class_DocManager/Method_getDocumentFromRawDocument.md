# Dcp\DocManager::getDocumentFromRawDocument() 

<div class="short-description">
Retourne un objet document en fonction des données brutes.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static string[] Dcp\DocManager::getDocumentFromRawDocument ( string[] $rawDocument) 

Retourne un objet document en fonction des données brutes. La classe de l'objet
retourné est fonction de la famille du document.

### Avertissements 

Aucun.

## Liste des paramètres 

(string[]) `rawDocument`
:   Données brutes d'un document.

## Valeur de retour 

Retourne un objet document en fonction des données brutes. La classe de l'objet
retourné est fonction de la famille du document.

## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception` :

*   si l'identifiant n'est pas
    syntaxiquement valide. L'identifiant doit être un nombre positif ou une chaîne
    de caractère non vide.
*   Si le tableau de donnée ne correspond pas à un document. Il doit contenir
    l'ensemble des propriétés.



## Historique 

Aucun.

## Exemples 

Conversion depuis `Dcp\DocumentManager::getRawDocument`.
La document `1234` est de la famille `MY_FAMILY`.

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    $rawDoc=\Dcp\DocumentManager::getRawDocument(1234);
    if ($rawDoc !== null) {
        // le titre
        print $rawDoc["title"];
        // l'attribut my_number1
        print $rawDoc[AMyFamily::my_number1];
        
        $doc=\Dcp\DocManager::getDocumentFromRawDocument($rawDoc);
        if ($doc !== null) {
            print $doc->getTitle();
        }
    }

## Notes 

Aucun appel en base de données est fait pour récupérer les données du document.

## Voir aussi 

*   `DocManager::getDocument()`
*   `DocManager::getRawDocument()`
