# Dcp\DocManager::getTitle() 

<div class="short-description">
Retourne le titre d'un document
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static string Dcp\DocManager::getTitle ( int|string $documentIdentifier,
                                   bool $latest=true)

Retourne le titre d'un document.

### Avertissements 

Cette méthode retourne le titre **brut**. Il peut différer du résultat de la
méthode `Doc::getTitle()` si cette dernière implémente un titre dynamique
fonction de paramètres externes au document.

Cette méthode n'utilise pas le cache. Le titre est issu de la base de données.

## Liste des paramètres 

(int|string) `documentIdentifier`
:   Identifiant numérique du document ou nom logique du document.


(bool) `latest` 
:   Utilisable que pour un identifiant numérique. Indique si on veut la
    révision précise correspondant à l'identifiant ou la dernière révision.

## Valeur de retour 

Le titre brute du document.
Pour les documents familles, le titre retourné est localisé.
Si l'identifiant ne correspond à aucun document `null` est retourné.

## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception`, si l'identifiant n'est pas
syntaxiquement valide. L'identifiant doit être un nombre positif ou une chaîne
de caractère non vide.


## Historique 

Remplace la fonction `getDocTitle`.

## Exemples 

    [php]
    $myTitle=\Dcp\DocumentManager::getTitle(1234);
    

## Notes 

Cette méthode est plus rapide que l'accès au titre à partir de
`DocManager::getDocument()` car elle ne charge pas l'objet Document en mémoire.

## Voir aussi 

*   `DocManager::getDocument()`
*   `DocManager::getRawDocument()`
