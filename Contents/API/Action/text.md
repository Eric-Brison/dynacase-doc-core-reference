# Action/text
 

## L'applicabilité ( marquer new / deprecated )

   Applicable

## Description courte

Retourne la traduction d'un texte.

## Description longue

La traduction prend en compte la locale de l'utilisateur (paramètre applicatif *CORE_LANG*). Ces traductions proviennent des catalogues produits dans les répertoires /locale/[fr,en]/LC_MESSAGES/. Le mécanisme de traduction utilise le mécanisme standard "*gettext*". Le fichier de catalogue utilisé est "freedom-catalog.mo". Ce fichier est produit et mis à jour à chaque mise à jour de module. Il contient l'ensemble des traductions pour l'ensemble des modules installés.

### Signature

    [php]
    public static function text(string $code):string

### Description


### Avertissements


## Liste des paramètres

code
: [in] (string) texte à traduire. Le texte à traduire doit être en US_ASCII (pas d'accents ni autres symboles).

## Valeur de retour

Si le texte à traduire est dans le catalogue, la traduction est retournée. L'encodage utilisé pour le retour est l'**UTF-8**.
Si le texte n'est pas trouvé dans le catalogue, le texte original est retourné.

## Erreurs / Exceptions


## Historique


## Exemples

    [php]
    $translate=Action::text("I speak english well ?");
    $lastValue="A34";
    $lastTranslate=sprintf(Action::text("My last value is %s"), $lastValue);

## Notes

La fonction PHP "_" peut aussi être utilisée pour récupérer une traduction si on est sûr que le texte à traduire est non vide. Car sinon, c'est l'entête du catalogue qui sera retourné.

Par défaut, seuls les catalogues français et anglais sont disponibles, mais il est possible de produire et d'ajouter d'autres catalogues de langue s'ils peuvent être écrits en UTF-8.

## See also

Voir le paragraphe *Internationalisation* pour ajouter des entrées aux catalogues de traductions.
