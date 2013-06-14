
# Paramétrage des droits applicatifs

Afin d'exécuter une [action][actionw], l'utilisateur doit disposer du 
[droit applicatif][acls] requis.

Les droits peuvent être défini avec le _centre d'administration_ ou par importation.

## Format d'importation de droit applicatif

Le format de fichier est :

*   [CSV][CSV]
    *   Encodage : UTF-8,
    *   Délimiteur de texte : ` ` (vide),
    *   séparateur de colonnes : `;`.
*   [ODS][ODS].


Le contenu du fichier suit la syntaxe suivante :

1.  `ACCESS` : mot-clef indiquant la pose d'un droit
1.  Identifiant du compte 
    *   Nom logique d'un document _Rôle_ (`ROLE`), _Groupe_ (`IGROUP`) ou _Utilisateur (`IUSER`) 
    *   Identifiant système numérique d'un compte. Ceci n'est pas l'identifiant 
        du document. C'est le numéro indiqué dans   l'attribut `us_whatid` du
         document correspondant.
1.  Nom de l'application
1.  Nom du droit applicatif
1.  Nom d'un autre droit, etc.

Exemple de fichier d'importation de droit applicatifs.

|  Clef  |    Compte    | Application |    Droit    |    Droit     |    Droit    |
| ------ | ------------ | ----------- | ----------- | ------------ | ----------- |
| ACCESS | MY_LITTEROLE | MY_APP      | MY_FIRSTACL | MY_SECONDACL |             |
| ACCESS | MY_BIGROLE   | MY_APP      | MY_FIRSTACL | MY_THIRDACL  | MY_EXTRAACL |
| ACCESS | MY_ADMINUSER | MY_APP      | MY_FIRSTACL | MY_ADMINACL  |             |

La clef `ACCESS` ne fait qu'ajouter des droits. L'importation ne permet pas de
supprimer les droits.

L'importation se fait par la commande [_wsh_][wshimport].

## Les droits applicatifs négatifs

Les droits applicatifs peuvent aussi être posés de manière à restreindre un accès
donné par un rôle ou un groupe.

Pour poser un droit applicatif négatif, il faut préfixer le nom du droit avec le
caractère _moins_ `-`.

Exemple :

|  Clef  |     Compte     | Application |    Droit     |     Droit     |    Droit    |
| ------ | -------------- | ----------- | ------------ | ------------- | ----------- |
| ACCESS | MY_BIGROLE     | MY_APP      | MY_FIRSTACL  | MY_THIRDACL   | MY_EXTRAACL |
| ACCESS | MY_BIGGROUP    | MY_APP      | -MY_THIRDACL |               |             |
| ACCESS | MY_SPECIALUSER | MY_APP      | -MY_EXTRAACL | MY_SPECIALACL |             |

Si :

*   L'utilisateur *MY_SPECIALUSER* est membre du groupe *MY_BIGGROUP*. 
*   Le rôle *MY_BIGROLES* est associé au groupe  *MY_BIGGROUP*.

Alors :

*   L'utilisateur *MY_SPECIALUSER* aura les droits *MY_FIRSTAC*L et *MY_SPECIALACL*
*   Les membres du groupes *MY_BIGGROUP* (autre que *MY_SPECIALUSER*) auront les 
    droits *MY_FIRSTACL* et *MY_EXTRAACL*.

<!-- links -->
[acls]:             #core-ref:a98b72ea-c063-4907-abc4-e5171ab55e59 "Déclaration de droits applicatifs"
[actionw]:          #core-ref:90bf0711-7874-4c9d-bdf0-7d28becb7628 "Déclaration d'une action"
[wshimport]:        #core-ref:1c97f553-dcba-454e-96a0-8059230065b3 "Importation par wsh"
[CSV]:              http://fr.wikipedia.org/wiki/Comma-separated_values "Comma-separated values sur wikipedia"
[ODS]:              http://fr.wikipedia.org/wiki/OpenDocument "Open Document sur wikipedia"