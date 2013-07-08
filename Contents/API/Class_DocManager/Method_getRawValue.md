# Dcp\DocManager::getRawValue() 

<div class="short-description">
Retourne la valeur brute d'une donnée de document.
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description 

    [php]
    static string getRawValue ( int|string $documentIdentifier,
                                    string $dataIdentifier
                                      bool $latest=true)

Retourne la valeur brute d'un attribut ou d'une propriété du document.

### Avertissements 

Cette méthode n'utilise pas le cache. La valeur est issue de la base de données.

## Liste des paramètres 

(int|string) `documentIdentifier`
:   Identifiant numérique du document ou nom logique du document.

(string) `dataIdentifier`
:   Identifiant de l'attribut ou de la propriété.

(bool) `latest` 
:   Utilisable que pour un identifiant numérique. Indique si on veut la
    révision précise correspondant à l'identifiant ou la dernière révision.


## Valeur de retour 

La valeur **brute** de l'attribut.

## Erreurs / Exceptions 

Exception `\Dcp\DocumentManager\Exception`

*   si l'identifiant n'est pas syntaxiquement valide. L'identifiant doit être un nombre positif ou une chaîne
    de caractère non vide.
*   si l'attribut n'existe pas 

Retourne chaîne vide si la valeur est vide.

## Historique 

Remplace partiellement `getDocValue`.
Pas de parcours de relation.

## Exemples 

    [php]
    use AMyFamily as \Dcp\AttributeIdentifiers\MyFamily
    $rawNumber=\Dcp\DocumentManager::getRawValue(1234, AMyFamily::my_number1);
    
    

## Notes 

Cette méthode est plus rapide et consomme moins de mémoire que
`DocManager::getDocument()` suivi de `Doc::getRawValue()`

Pas de vérification que l'identifiant est un attribut du document.
L'identifiant peut être toutes données présentes dans la base. Ceci inclus les
propriétés.

## Voir aussi 

*   `Doc::getRawValue()`
