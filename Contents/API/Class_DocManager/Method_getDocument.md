# Dcp\DocManager::getDocument() 

<div class="short-description">
Retourne un document en fonction de son identifiant.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static Dcp\Family\Document getDocument ( int|string $documentIdentifier,
                                                   bool $latest=true,
                                                   bool $useCache=true )

Retourne un objet _Document_ en fonction de son identifiant et de sa famille.

### Avertissements 

Les droits d'accès ne sont pas vérifiés.

## Liste des paramètres 

(int|string) `documentIdentifier`
:   Identifiant numérique du document ou nom logique du document.

(bool) `latest` 

:   Utilisable que pour un identifiant numérique. Indique si on veut la
    révision précise correspondant à l'identifiant ou la dernière révision.

(bool) `useCache`

:   Par défaut, la cache est activé. Cela signifie que le document est récupéré
    du cache s'il est présent dans celui-ci. Sinon, les données du document sont 
    récupérées de la base de données et mises dans le cache.  
    Si `useCache` est mis à `false`, le données du document sont systématiquement
    récupérées de la base de données et le cache n'est pas utilisé.


## Valeur de retour 

Retourne un objet de la classe de la famille qui correspond au document.
Si l'identifiant ne correspond à aucun document `null` est retourné.

## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception`, si l'identifiant n'est pas
syntaxiquement valide. L'identifiant doit être un nombre positif ou une chaine
de caractère non vide.

## Historique 

Remplace la fonction `new_Doc`.

## Exemples 

### Accès par identifiant

Identifiant numérique :

    [php]
    $doc=\Dcp\DocumentManager::getDocument(1234);
    if ($doc !== null && $doc->isAlive()) {
        if ($doc->hasPermission('view')) {
            print $doc->getTitle();
        }
    }

Nom logique :

    [php]
    $doc=\Dcp\DocumentManager::getDocument('MY_DOCUMENT');
    if ($doc !== null && $doc->isAlive()) {
        if ($doc->hasPermission('view')) {
            print $doc->getTitle();
        }
    }


### Utilisation du cache

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    function myFirst() {
        $doc=\Dcp\DocumentManager::getDocument(1234);
        if ($doc !== null && $doc->isAlive()) {
            $doc->setAttributeValue(AMyFamily::my_number1, 324)
        }
    }
    function mySecond() {
        $doc=\Dcp\DocumentManager::getDocument(1234);
        if ($doc !== null && $doc->isAlive()) {
            $doc->setAttributeValue(AMyFamily::my_number2, 765)
        }
    }
    function myFinal() {
        myFirst();
        mySecond();
        $doc=\Dcp\DocumentManager::getDocument(1234);
        if ($doc !== null && $doc->isAlive()) {
            $n1=$doc->getAttributeValue(AMyFamily::my_number1);
            // n1 vaut 324
            $n2=$doc->getAttributeValue(AMyFamily::my_number2);
            // n2 vaut 765
            $doc->setAttributeValue(AMyFamily::my_sum, ($n1 + $n2));
            // la somme est de 1089
            $doc->store();
        }
    }

## Notes 

L'utilisation du cache nécessite de la mémoire. Il faut éviter d'utiliser le cache
dans une boucle qui potentiellement va instancier de nombreux documents.

Pour une utilisation en boucle, il est préférable d'utiliser les classes
`DocumentList` ou `SearchDoc` qui manipule des listes de documents.


## Voir aussi 

*   `DocManager::getRawDocument()`
