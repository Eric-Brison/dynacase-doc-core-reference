# Paramétrage des droits documentaires {#core-ref:a99dcc5f-f42f-4574-bbfa-d7bb0573c95d}

## Le profil de documents {#core-ref:f1575705-10e8-4bf2-83b3-4c0b5bfb77cf}

Le profil permet de déterminer les droits acquis pour les rôles, les groupes et
les utilisateurs.

Le profil contient la matrice permettant d'associer _comptes_ et _droits_.

Exemple de matrice de droits :

|                |                   Droit D1                  |                   Droit D2                  |                   Droit D3                  |
| -------------- | :-----------------------------------------: | :-----------------------------------------: | :-----------------------------------------: |
| Rôle R1        | <span class="aclgreen">X</span> |                                             | <span class="aclgreen">X</span> |
| Rôle R2        |                                             | <span class="aclgreen">X</span> |                                             |
| Groupe G1      | <span class="aclgreen">X</span> |                                             |                                             |
| Utilisateur U1 |  <span class="aclgrey">O</span> |  <span class="aclgrey">O</span> |  <span class="aclgrey">O</span> |
|                |                                             |                                             |                                             |



Quatre familles de profils sont définies :

*   profil de famille (droit de créer des documents ou de voir la famille)
*   profil de document (droit de voir, modifier ou supprimer des documents)
*   profil de dossier (droit de voir le contenu du dossier)
*   profil de recherche (droit d'exécuter la recherche)


Liste des droits définis pour ces quatre familles de profils :

Légende :

*    `D` : Pour les profils de Document
*    `F` : Pour les profils de Dossier (_Folder_)
*    `S` : Pour les profils de Recherche (_Search_)
*    `C` : Pour les profils de Famille

| Nom interne  |        Description         |                                                                                                                                                                                                                  Description longue                                                                                                                                                                                                                  | `D` | `F` | `S` | `C` |
| ------------ | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- | --- | --- | --- |
| view         | voir                       | Voir les caractéristiques du document, du dossier ou de la recherche. Le fait de ne pas voir un dossier n'implique pas de ne pas voir les documents contenus dans le dossier.                                                                                                                                                                                                                                                                        | X   | X   | X   |     |
| edit         | modifier                   | Modifier les caractéristiques du document, du dossier.                                                                                                                                                                                                                                                                                                                                                                                               | X   | X   | X   |     |
| delete       | supprimer                  | Supprimer le document, le dossier, la recherche; c'est à dire le mettre à la poubelle.                                                                                                                                                                                                                                                                                                                                                               | X   | X   | X   |     |
| send         | envoyer                    | Envoyer par courriel le document.                                                                                                                                                                                                                                                                                                                                                                                                                    | X   |     |     |     |
| unlock       | déverrouiller              | déverrouiller le document.                                                                                                                                                                                                                                                                                                                                                                                                                           | X   | X   | X   |     |
| viewacl      | voir les droits            | Voir les droits du document.                                                                                                                                                                                                                                                                                                                                                                                                                         | X   | X   | X   |     |
| modifyacl    | modifier les droits        | Modifier les droits du document.                                                                                                                                                                                                                                                                                                                                                                                                                     | X   | X   | X   |     |
| open         | ouvrir                     | Ouvrir le dossier. Permet de voir le contenu du dossier                                                                                                                                                                                                                                                                                                                                                                                              |     | X   |     |     |
| modify       | modifier                   | Modifier le contenu du dossier. Permet d'ajouter ou de supprimer des documents dans le dossier.                                                                                                                                                                                                                                                                                                                                                      |     | X   |     |     |
| execute      | executer                   | Permet d'exécuter la recherche.                                                                                                                                                                                                                                                                                                                                                                                                                      |     |     | X   |     |
| create       | créer                      | Autorise la création de document de cette famille.                                                                                                                                                                                                                                                                                                                                                                                                   |     |     |     | X   |
| icreate      | créer manuellement         | Autorise la création de document de cette famille à partir de l'interface. Si ce droit n'est pas mis est que create est mis, l'utilisateur ne pourra créer le document que de manière indirecte (soit sur une transition, soit sur toutes autres actions particulière mis en place par l'administrateur). Sans ce droit les menus de création de cette famille sont inaccessibles. Si ce droit est mis il faut que le droit 'create' soit aussi mis. |     |     |     | X   |
| confidential | voir document confidentiel | Permet d'utiliser normalement un document qui est confidentiel. (Confidentiel est une propriété de document).                                                                                                                                                                                                                                                                                                                                        | X   | X   | X   |     |


## Profil liés {#core-ref:edc17da5-bc7c-4d13-9887-e75a9d5ee519}

Un document _Profil_ est fait pour être appliqué à des documents. Un document
qui est lié à un profil obtient les mêmes droits que ceux définis sur le profil.
Dès que les droits du profils sont changés alors tous les documents liés à ce
profils ont aussi leur droits changés.

Une famille peut indiquer un [profil par défaut][CPROFID] pour les documents de
cette famille. Une fois cette propriété de famille enregistrée, tous les
documents seront liés avec le même profil.

**Un document sans profil n'est pas protégé.** Il est alors accessible est
modifiable pour tous les utilisateurs.

### Lier un profil par fichier d'importation {#core-ref:f48b4516-ded5-4452-9f35-f55e87e8a370}

Le profil d'un document peut être modifié avec un fichier d'importation en
utilisant la clef `PROFID`. La syntaxe est celle décrite pour 
l'[exportation de profil][exportprofid].


|            | Identifiant du document | Identifiant du profil |
| ---------- | ----------------------- | --------------------- |
| __PROFIL__ | MY_DOCUMENT             | MY_PROFIL             |


### Affecter les droits d'un profil par importation {#core-ref:2ec1ae6f-4b2a-4bc2-a100-4e5873538bb5}

Un droit peut être posé sur un rôle, un groupe ou un utilisateur. Pour indiquer
ce compte il faut utiliser le nom logique du document lié à ce compte ou
l'identifiant système du compte (attribut _us_whatid_ donné sur le document).

Trois options permette de poser les rôles :

*   ADD : Ajout de droits, les anciens droits sont conservés (option par défaut)
*   DELETE :   Supprime des droits
*   RESET : Efface les droits avant de les ajouter

Chaque droit posé est déclaré après la quatrième colonne. Pour chacun des
droits, un ou plusieurs identifiant de compte doit être indiqué. Si plusieurs
comptes sont associés à un droit ils doivent être dans la même cellule séparés
par une virgule ou alors dans des cellules séparées.

|            | Identifiant du profil |  /  | Option |       Droit       |       Droit       |       Droit        |
| ---------- | --------------------- | --- | ------ | ----------------- | ----------------- | ------------------ |
| __PROFIL__ | MY_PROFIL             |     | RESET  | view=GALL, GADMIN | edit=GADMIN       | delete=GADMIN      |
| __PROFIL__ | MY_OTHER_PROFIL       |     |        | view=GALL         | edit=MY_FIRSTROLE | view=MY_FIRSTGROUP |
|            |                       |     |        |                   |                   |                    |

### Lier un profil par programmation {#core-ref:b8065dc8-8f14-4749-91a8-a07acc671f1a}

La méthode `Doc::setProfil($profilIdentifier)` permet de lier un profil à un
document.

**Note** : Un document _Profil_ ne peut pas être lié à un autre profil.

## Profil dédié {#core-ref:25c54b68-9cc1-44ea-b203-e289bde65a12}

Un document qui porte son propre profil est déclaré comme _profil dédié_. Cela
implique que la modification du profil du document n'impactera que lui-même.

Les documents "_profil_" ont tous des profils dédiés.

En utilisant un fichier d'importation, l'exemple suivant déclare un profil dédié.

|            | Identifiant du document | Identifiant du profil |
| ---------- | ----------------------- | --------------------- |
| __PROFIL__ | MY_DOCUMENT             | MY_DOCUMENT           |



## Profil dynamique {#core-ref:bc24834a-b380-4681-ae94-08b93076a7e8}

Un document _profil_ est _dynamique_ si l'attribut "dynamique/famille"
(`dpdoc_famid`) est valorisé. Cet attribut doit contenir un identifiant de
famille. Dans ce cas, ce profil ne pourra être lié qu'à un document de cette
famille ou derivée de cette famille.

Cette caractérique permet de rajouter des droits en fonction des attributs
_[account][accounttype]_ présents dans le document. Les attributs de type
_[docid][docidtype]_ avec l'option "isuser=yes" sont aussi utilisables comme
paramètre de droit.

Exemple :

| BEGIN |                    |      Recette      |                |     | TST_RECETTE |         |     |     |      |      |         |         |       |            |             |
| ----- | ------------------ | ----------------- | -------------- | --- | ----------- | ------- | --- | --- | ---- | ---- | ------- | ------- | ----- | ---------- | ----------- |
| //    | idattr             | idframe           | label          | T   | A           | type    | ord | vis | need | link | phpfile | phpfunc | elink | constraint | option      |
|       |                    |                   |                |     |             |         |     |     |      |      |         |         |       |            |             |
| ATTR  | TST_IDENTIFICATION |                   | Identification | N   | N           | frame   | 100 | W   |      |      |         |         |       |            |             |
| ATTR  | TST_SUBJECT        | AN_IDENTIFICATION | Sujet          | Y   | N           | text    | 110 | W   | Y    |      |         |         |       |            |             |
| ATTR  | TST_WRITER         | AN_IDENTIFICATION | Rédacteur      | N   | N           | account | 120 | W   |      |      |         |         |       |            |             |
| ATTR  | TST_OBSERVERS      | AN_IDENTIFICATION | Observateurs   | N   | N           | account | 130 | W   |      |      |         |         |       |            | match=group |
|       |                    |                   |                |     |             |         |     |     |      |      |         |         |       |            |             |

Dans cette famille, le rédacteur le groupe d'observateur peuvent être utilisés
dans la définition des droits. Il est possible d'avoir les règles suivantes :

*   le rédacteur a le droit de voir et de modifier le document
*   les observateurs ont le droit de voir le document

Si le rédacteur est modifié alors les droits sur le document sont aussi
modifiés. De même si un utilisateur devient membre de groupe référencé par
l'attribut `tst_observers` alors il aura le droit de voir ce document.

L'importation de droit pour un profil dynamique se fait en utilisant
l'identifiant de l'attribut à la place de l'identifiant d'un rôle, d'un groupe
ou d'un utilisateur. Un profil dynamique peut aussi avoir une partie statique
comme les profils standards.

|            | Identifiant du profil |  /  | Option |             Droit              |      Droit      |     Droit     |
| ---------- | --------------------- | --- | ------ | ------------------------------ | --------------- | ------------- |
| __PROFIL__ | MY_DYNAMIC_PROFIL     |     | RESET  | view=tst_writer, tst_observers | edit=tst_writer | delete=GADMIN |

## Profil privé {#core-ref:1a8bca3d-2599-4ef7-8f31-e58b36ee1588}

Le profil privé est un profil personnel associé à chacun des utilisateurs. C'est
un profil de dossier. Il est applicable aussi aux documents.

Le nom logique de ce profil est `PERSONAL-PROFIL-<uid>`. `uid` est l'identifiant
système du compte.

La fonction `getMyProfil()` permet de récupérer le profil privé de l'utilisateur
courant. Par défaut, le profil privée donne tous les droits à l'utilisateur
associé et aucun autre. L'utilisateur peut alors décider d'ajouter d'autre
groupes ou d'autre utilisateur à son profil pour accéder à ces documents privés.




<!-- links -->
[authentification]: #core-ref:b482b82b-ebe2-46e4-8051-c6e83d11a2ae
[actiondef]:        #core-ref:7fcd8c91-b981-4ef6-b4b5-7975a17dbe73 "Définition d'une action"
[suppleant]:        #core-ref:1591eb1c-aead-4f7b-bde9-5f42e397b22e
[users]:            #core-ref:02f32b3d-be94-44f7-9b98-879c6b551c4a
[groups]:           #core-ref:d3a9acde-f4fa-4a0b-8acc-1303f8e6b17e
[roles]:            #core-ref:b9742040-0367-4a3d-a411-7195ec5fa7a4
[guest]:            #core-ref:932e2070-6929-11e2-8218-0021e9fffec1
[document]:         #core-ref:67929e29-abef-437c-88a3-7f43647c60ff "Définition d'un document"
[acls]:             #core-ref:a98b72ea-c063-4907-abc4-e5171ab55e59 "Déclaration de droits applicatifs"
[actionw]:          #core-ref:90bf0711-7874-4c9d-bdf0-7d28becb7628 "Déclaration d'une action"
[wshimport]:        #core-ref:1c97f553-dcba-454e-96a0-8059230065b3 "Importation par wsh"
[CSV]:              http://fr.wikipedia.org/wiki/Comma-separated_values "Comma-separated values sur wikipedia"
[ODS]:              http://fr.wikipedia.org/wiki/OpenDocument "Open Document sur wikipedia"
[CPROFID]:          #core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3 "Propriété CPROFID"
[exportprofid]:     #core-ref:602c6331-7cdb-4b24-8a56-ffd11e00502f "Exportation de profils"
[accounttype]:      #core-ref:87230967-8155-421c-8bbe-70a3c1adc3c0
[docidtype]:        #core-ref:d461d5f5-b635-47a0-944d-473c227587ab
