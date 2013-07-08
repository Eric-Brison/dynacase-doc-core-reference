# Dcp\DocManager::createTemporaryDocument() 

<div class="short-description">
Créé un objet document temporaire.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static Dcp\Family\Document createTemporaryDocument(
          int|string $familyIdentifier,
                bool $useDefaultValues`=true) 

Créer un objet de document temporaire. La classe de l'objet retourné est
fonction de la famille du document. L'objet document n'a pas encore
d'identifiant. Son identifiant **temporaire** sera donné lors de
l'enregistrement (`Doc::store()`).

Un identifiant temporaire n'a qu'une durée de vie d'une journée. Cet identifiant
est réutilisable dès que la suppression du document temporaire a été effectuée
par le programme de nettoyage.

Un document temporaire n'a pas de droit.

### Avertissements 

Le document n'est pas mis en cache.
Les droits ne sont pas vérifiés.

Les documents temporaires sont supprimés toutes les nuits.

## Liste des paramètres 


(int|string) `familyIdentifier`
:   Identifiant de la famille du document à créer

    
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

Remplace la fonction `createTmpDoc`.

## Exemples 

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    use MyFamily as \Dcp\Family\MyFamily
    $doc=\Dcp\DocumentManager::createTemporaryDocument(MyFamily::familyName);
    $doc->setAttributeValue(AMyFamily::my_number1, 345);
    $doc->setAttributeValue(AMyFamily::my_number2, 654);
    $err=$doc->store();
    if (empty($err)) {
        printf("Nouveau document temporaire %s n°%d", $doc->getTitle(), $doc->id);
    }

## Notes 

Le document temporaire peut aussi servir pour réaliser des opérations sans pour
autant nécessiter un enregistrement en base de données.

## Voir aussi 

*   \Dcp\DocManager\createDocument
