# Dcp\DocManager::createDocument() 

<div class="short-description">
Créé un objet document.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static Dcp\Family\Document createDocument(
          int|string $familyIdentifier,
                bool $control=true,
                bool $useDefaultValues`=true) 

Créer un objet de document. La classe de l'objet retourné est fonction de la
famille du document. L'objet document n'a pas encore d'identifiant. Son
identifiant sera donné lors de l'enregistrement (`Doc::store()`).

### Avertissements 

Le document n'est pas mis en cache.

## Liste des paramètres 


(int|string) `familyIdentifier`
:   Identifiant de la famille du document à créer

(bool) `control`
    Indique s'il faut vérifier le droit de créer. 
    
(bool) `useDefaultValues`
    Indique s'il initiliser les attributs avec leurs valeurs par défaut.


## Valeur de retour 

Retour un objet de la classe de la famille indiquée.


## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception` :

*    Si l'identifiant de famille n'est     pas syntaxiquement valide.
    L'identifiant doit être un nombre positif ou une  chaine de caractère non
    vide.
*   Si la famille n'existe pas.
*   Si le droit de créer n'est pas accordé (droit `create`). 



## Historique 

Remplace la fonction `createDoc`.

## Exemples 

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    use MyFamily as \Dcp\Family\MyFamily
    $doc=\Dcp\DocumentManager::createDocument(MyFamily::familyName);
    $doc->setAttributeValue(AMyFamily::my_number1, 345);
    $doc->setAttributeValue(AMyFamily::my_number2, 654);
    $err=$doc->store();
    if (empty($err)) {
        printf("Nouveau document %s n°%d", $doc->getTitle(), $doc->id);
    }

## Notes 



## Voir aussi 

*   \Dcp\DocManager\createTemporaryDocument
