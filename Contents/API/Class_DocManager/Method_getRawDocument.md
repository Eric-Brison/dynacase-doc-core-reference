# Dcp\DocManager::getRawDocument() 

<div class="short-description">
Retourne les valeurs et les propriétés brutes d'un document.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static string[] Dcp\DocManager::getRawDocument (  int|string $documentIdentifier,
                                                   bool $latest=true )

Retourne un tableau de valeurs de document issus de la base de données.

### Avertissements 

Un accès à la base de donnée est systématiqument effectué.

Les droits d'accès ne sont pas vérifiés.

## Liste des paramètres 

(int|string) `documentIdentifier`
:   Identifiant numérique du document ou nom logique du document.

(bool) `latest` 

:   Utilisable que pour un identifiant numérique. Indique si on veut la
    révision précise correspondant à l'identifiant ou la dernière révision.
 

## Valeur de retour 

Tableau de valeurs brutes. L'index du tableau contient l'identifiant de la
propriétés ou de l'attribut. Tous les identifiants sont en minucules.

## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception`, si l'identifiant n'est pas
syntaxiquement valide. L'identifiant doit être un nombre positif ou une chaine
de caractère non vide.

## Historique 

Remplace le fonction `getTDoc`.

## Exemples 

### Accès par identifiant

Identifiant numérique :
La document `1234` est de la famille `MY_FAMILY`.

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    $rawDoc=\Dcp\DocumentManager::getRawDocument(1234);
    if ($rawDoc !== null) {
        // le titre
        print $rawDoc["title"];
        // l'attribut my_number1
        print $rawDoc[AMyFamily::my_number1];
    }

## Notes 

Cet méthode est plus rapide et consomme moins de mémoire que
`DocManager::getDocument()` suivi de `Doc::getTitle()`

## Voir aussi 

*   `Dcp\DocManager::getDocument()`
