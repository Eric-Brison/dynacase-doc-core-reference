# Importation de documents CSV {#core-ref:2fb3284a-2424-44b2-93ae-41dc3969e093}
 
Ce chapitre indique comme importer des documents au format
 _[CSV][CSV]_ ou _[ODS][ODS]_.

## Constitution du fichier d'importation {#core-ref:31f163da-2878-43b9-9056-a17b63bdc114}
Le fichier d'importation peut être au format : 

* CSV (séparateur de champ **point-virgule** , séparateur de texte vide) avec un encodage UTF-8
* ODS OpenDocument Spreadsheet (tableur OpenOffice.org .ods)


#### Ordre des attributs  {#core-ref:e41116ee-a682-4033-a7ab-22dc1b99e56a}

Avant de décrire les valeurs des attributs d'un document il est nécessaire
d'indiquer à quels attributs correspond la valeur.



 

Pour définir l'ordre des attributs, il faut définir une ligne `ORDER` par
famille (une ligne `ORDER` ne peut pas être utilisée pour deux familles
différentes même si elles sont héritées). Les `ORDER` sont propres à chaque
famille. Il doit être présent avant les lignes décrivant les  documents.

Les 4 premières colonnes sont toujours les mêmes : 

1. 1ère colonne : toujours `ORDER`,
1. 2ème colonne : identifiant de la famille ,
1. 3ème colonne : vide (utilisée pour l'alignement avec la ligne `DOC`) 
1. 4ème colonne : vide (utilisée pour l'alignement avec la ligne `DOC`)

Les autres colonnes définiront l'ordre des attributs à utiliser dans les 
 lignes DOC de la même famille qui suivront.


 Si plusieurs lignes `ORDER` sont écrites à la suite, les documents
sont importés avec le dernier ordre interprété.

Exemple : 

|     #     |    famille     |     |     |                   |                      |                      |
| --------- | -------------- | --- | --- | ----------------- | -------------------- | -------------------- |
| **ORDER** | **ZOO_CLASSE** |     |     | **cl_latinname**  | **cl_commonname**    | **cl_caracteristic** |
| DOC       | ZOO_CLASSE     |     | -   | Actinopterygii    | Poissons             | Nage                 |
| DOC       | ZOO_CLASSE     |     | -   | Reptilia          | Reptiles             | Rampe                |
|           |                |     | -   |                   |                      |                      |
| **ORDER** | **ZOO_CLASSE** |     |     | **cl_commonname** | **cl_caracteristic** | **cl_latinname**     |
| DOC       | ZOO_CLASSE     |     | -   | Oiseaux           | Vole                 | Aves                 |
| DOC       | ZOO_CLASSE     |     | -   | Mammifères        | Allaite              | Mammalia             |


Dans ce cas, les deux premiers documents utilisent le
premier `ORDER`, et les documents suivants le deuxième `ORDER` (la deuxième ligne
`ORDER` a écrasé les directives de la première). 


### Description d'un document {#core-ref:3acb8fbe-6e5a-4933-95fa-2cea0eae2fc5}

Les quatre premières colonnes définissent les paramètres du document : 

1. 1ère colonne : toujours `DOC` ,
1. 2ème colonne : identifiant de la famille,
1. 3ème colonne : identifiant du document. Utiliser un identifiant existant 
   indique une modification du document existant. Un identifiant vide ou égal
    à zéro indique une création de document, 
1. 4ème colonne : identifiant du dossier où insérer le document. Si un 
   identificateur est précisé le document est référencé dans le dossier
   (s'il n'y est pas déjà). Si l'identificateur n'est pas précisé (vide ou zéro),
   le document est référencé dans le dossier courant (celui qui est sélectionné 
   dans l'arborescence en cas d'utilisation avec l'interface web d'importation). 
   Si l'identifiant est '-' alors il ne sera référencé dans aucun dossier. 

Les colonnes suivantes décrivent les valeurs **brutes** des
attributs du document.

#### Valeurs des attributs pour l'importation

Les valeurs inscrites dans le document sont insérés avec
la méthode "Doc::getRawValue()".

Les attributs relations (`docid`, `account`, `thesaurus`) peuvent contenir soit
le nom logique de la cible soit son identifiant système. Dans ce dernier cas,
l'importation  sera valide que pour un contexte donnée.

Les attributs de type énuméré (`enum`) doivent contenir la clef et non le libellé.

Les dates (`date`, `timestamp`) doivent être renseignés au format ISO (`YYYY-MM-
DD`  ou `YYYY-MM-DD HH:MM:SS` ou `YYYY-MM-DDTHH:MM:SS`).   
Si la date est au format `DD/MM/YYYY`,  il faut dans ce cas que la locale de
l'utilisateur soit en français (`CORE_LANG=fr_FR`).  De même, si la date est au
format `MM/DD/YYYY`, la locale de l'utilisateur doit être `en_US`. Dans tous ces 
cas la valeur de la date stockée sera au format ISO.

Les attributs multivalués (contenu dans un tableau ou avec option
`multiple=yes`) doivent séparer chacune de leur valeur par les deux caractères
`\n`. Les caractères `<BR>` sont considérés comme des retours chariots dans le
cas des attributs multiples.   Pour les attributs multivalués à deux niveaux
(attribut contenu dans un tableau   avec l'option `multiple=yes`), les
caractères `<BR>` servent de séparateur de   deuxième niveau.

 Exemple : soit la relation suivante : `1236\n6375<BR>8755<BR>564\n567<BR><BR>4569` 
 donnera la structure suivante :
 
 | index |        relations        |
 | ----- | ----------------------- |
 |     1 | 1236                    |
 |     2 | 6375<br />8755<br />564 |
 |     3 | 567<br /><br />4569     |


#### Hameçons déclenchés lors de l'importation

Les [hameçons][hooks] sont lancés après avoir mis à jour les valeurs du document
dans l'objet documentaire.

Lors d'un ajout de documents les hameçons suivants sont lancés :

1. preRefresh()
1. postRefresh()
1. preImport($extra)
1. preCreated()
1. postCreated()
1. postStore()
1. postImport($extra)

Lors d'une mise à jour de documents les hameçons suivants sont lancés :

1. preRefresh()
1. postRefresh()
1. preImport($extra)
1. postStore()
1. postImport($extra)


**Note** : Les contraintes ne sont pas vérifiées lors de l'importation des
documents.  De même, le caractère obligatoire des attributs n'est pas vérifié
non plus.

#### Informations supplémentaires {#core-ref:15088f40-de05-4600-86bb-82422af01dce}

 Lors de l'importation d'un document, il est
possible d'indiquer des informations supplémentaires pour réaliser des
traitements conditionnels lors de l'importation. 

Les attributs ayant une clé commençant par `extra:` seront enregistrés comme
attribut extra.  Les attributs _extra_ sont passés en paramètre des méthodes
`preImport` et `postImport` de la famille associée, sous forme d'un tableau
associatif de forme clé => valeur, avec pour clé la chaîne de caractères suivant
le 'extra:' dans la description du nom de l'attribut, et comme valeur, celle
correspondante à cette colonne.

Exemple :


|     #     |    famille     |     |     |                  |                  |                   |
| --------- | -------------- | --- | --- | ---------------- | ---------------- | ----------------- |
| **ORDER** | **ZOO_CLASSE** |     |     | **cl_latinname** | **extra:status** | **extra:special** |
| DOC       | ZOO_CLASSE     |     | -   | Actinopterygii   | alive            | protected         |
|           |                |     |     |                  |                  |                   |

Dans cette exemple, le document Actinopterygii de la famille ZOO_CLASSE aura
comme paramètre passé à `preImport` et `postImport` : 

    [php]
    array('state' => 'alive',
          'special' => 'protected');


### Clés d'importation {#core-ref:7eefc8e7-16a6-4188-99d5-c2c9d817a1fe}

Chaque famille peut aussi posséder une ligne `KEYS`. Une ligne `KEYS` ne peut
pas être utilisée pour deux familles différentes. Cette ligne permet de définir
les clés qui seront utilisées pour reconnaître le document. Si la troisième
colonne (identifiant) d'une ligne `DOC` est vide (pas de nom logique pour le
document), et que l'option d'importation est à **_mise à jour_** (option par
défaut), alors la clé sera utilisée pour retrouver le document.

La clé utilisée par défaut pour reconnaître le document est la propriété `title`
de ce document. Si un et un seul document de la même famille contient les mêmes
valeurs que celles définis dans les attributs `KEYS`, alors le document sera mis
à jour avec les informations d'importation de cette ligne.

L'ordre des colonnes est  :

1. 1ère colonne : toujours `KEYS`,
1. 2ème colonne : Identifiant de la famille,
1. 3ème colonne : vide,
1. 4ème colonne : vide,
1. 5ème colonne : clef primaire,
1. 6ème colonne : clef secondaire.

Les colonnes 5 et 6 servent à définir les attributs qui seront utilisés comme
clé.  On peut avoir un maximum de deux clés par ligne (dans ce cas, il faudra
que les deux clés correspondent pour que le document soit reconnu)

Exemple :

|     #     |    famille     |     |     |                  |                   |                      |
| --------- | -------------- | --- | --- | ---------------- | ----------------- | -------------------- |
| **ORDER** | **ZOO_CLASSE** |     |     | **cl_latinname** | **cl_commonname** | **cl_caracteristic** |
| **KEYS**  | **ZOO_CLASSE** |     |     | **cl_latinname** |                   |                      |
| DOC       | ZOO_CLASSE     |     | -   | Actinopterygii   | Poissons          |                      |
| DOC       | ZOO_CLASSE     |     | -   | Reptilia         | Reptiles          | Rampe                |
| DOC       | ZOO_CLASSE     |     | -   | Actinopterygii   |                   | Nage                 |

Dans cette exemple, les documents seront reconnus par leur attribut
'cl_latinname'. Donc pour le premier document, la clé sera
'Actinopterygii', et pour le deuxième 'Reptilia'. Dans cet exemple le document 
_Actinopterygii_ sera d'abord créé avec le nom _Poissons_, puis il sera mis à jour 
avec la caractéristique _Nage_.

Les lignes `KEYS` seront appliquées dans l'ordre dans
lesquelles elles ont été écrites.

## Modifier l'icone d'un document {#core-ref:ac8ef5d6-fd4f-403e-bec1-486466f3f5f7}

Bien que généralement l'icone d'un document provient de sa famille, il est possible 
de modifier de manière spécifique l'icone d'un document en particulier avec la 
clef `DOCICON`.

L'ordre des colonnes est  :

1. 1ère colonne : toujours `DOCICON`,
1. 2ème colonne : identifiant du document (nom logique),
1. 3ème colonne : nom du fichier image.

|     #     |    famille     |          |     |                  |                   |                      |
| --------- | -------------- | -------- | --- | ---------------- | ----------------- | -------------------- |
| **ORDER** | **ZOO_CLASSE** |          |     | **cl_latinname** | **cl_commonname** | **cl_caracteristic** |
| DOC       | ZOO_CLASSE     | CL_ACTI  | -   | Actinopterygii   | Poissons          |                      |
| DOCICON   | CL_ACTI        | fish.png | -   |                  |                   |                      |

Le nom de l'image doit référencer un fichier présent dans le répertoire `Images`
à  la racine du répertoire d'installation sur le serveur.



<!-- links -->
[CSV]: http://fr.wikipedia.org/wiki/Comma-separated_values "Comma-separated values sur wikipedia"
[ODS]: http://fr.wikipedia.org/wiki/OpenDocument "Open Document sur wikipedia"
[hooks]: #core-ref:8f3d47de-32b5-4748-8a00-b1569c5423e5