# Exportation de documents {#core-ref:88fb91b5-51a3-4b33-ac2e-5f20eddd8210}
 
L'accès à l'interface d'exportation se fait depuis le _centre d'administration_.
avec l'application _Explorateur de documents_.

![ Exportation de documents ](ihmexportation.png)

Pour exporter, il faut cliquer sur le menu _Outils/Exportation_ du dossier depuis
la fenêtre d'ouverture de dossier (ou de recherche). L'accès à l'exportation est
aussi disponible sur le menu contextuel affichable en cliquant sur les icônes de
dossier ou de recherche présentes dans l'arborescence.


Options d'exportation :

Encodage 
:   Deux encodages sont proposés. Cela est nécessaire pour les valeurs
textuelles qui comportent des accents. Si votre poste client est sur le système
Windows et que vous voulez utiliser MicroSoft Excel, il est préférable de
choisir `ISO 8859-15`. Sinon pour openOffice.org il est conseillé d'utiliser
`UTF-8`. Lors d'une [importation][ImportationCSV]  l'encodage est détecté
automatiquement et ces 2 encodages sont supportés.

Profil

:   Cela permet de sauvegarder les profils associés à un document. Seuls les profils
des documents avec profils dédiés (généralement les documents profils) sont
exportés. Cette option est utile lorsqu'un concepteur de famille veut
récupérer son [paramétrage profil][exportprofil].

Fichiers 

:   L'option sans les fichiers indique que seul le fichier _csv_
contenant les valeurs des attributs sera exporté. Les fichiers liés aux
attributs de type [file][attrfile] ou [image][attrimage] ne sont pas exportés.
    
    L'option avec les fichiers indique que l'exportation générera un fichier
archive de type Zip. Cette archive contiendra le fichier `fdl.csv` qui contient
les valeurs des attributs et les fichiers attachées aux documents exportés.
Cette archive peut être réimporté à l'[importation d'archive][importArchive].
Pour des raisons de compatibilité avec les différents systèmes d'exploitations
les noms des fichiers exportés ne comportent pas d'accents

Identificateur 

:   Permet de sauvegarder les identificateurs systèmes numériques
des documents. Cela implique que votre fichier ne sera ré-importable que dans la
même base. Cela identifie de manière non ambiguë le document dans l'objectif
d'une restauration. Dans tous les cas, si les documents comportent des noms
logiques (propriété `name`), ces noms sont exportés à la place des identifiants
systèmes.

Choisir les colonnes 

:   Cette option permet d'exporter que certains attributs du documents. Chaque
administrateur  peut définir et sauvegarder les attributs qu'il veut exporter.
L'interface de choix  des colonnes est présentés lorsqu'une famille est
sélectionnée. Une fois le choix  sélectionné et sauvegardé alors seuls les
attributs choisis seront exportés. Le  choix _"Ne pas tenir compte des
préférences"_ permet d'exporter l'ensemble des attributs.


## Différents formats d'exportation {#core-ref:e51257aa-3a16-41be-94ed-7ef2206a899b}
  
### Données réimportables {#core-ref:aa0070b2-5d64-4882-b083-acd05450059a}

Le fichier produit est un fichier _csv_ conforme au format d'[importation
CSV][ImportationCSV] si l'option _Sans les fichiers_ est choisi. 

Le séparateur de champ est le point-virgule `;` et le séparateur de texte est
vide.

L'option _sans les fichiers_ indique que seul le fichier _csv_ contenant les
valeurs des attributs sera exporté. Les fichiers liés aux attributs de type
[file][attrfile] ou [image][attrimage] ne sont pas exportés.

Exemple de fichier _csv_ produit : (ici avec l'option _avec les identificateurs_)
    
| //FAM | animal(ZOO_ANIMAL) | Identifiant | Dossier |   nom    |    espèce    |   classe  |
| ----- | ------------------ | ----------- | ------- | -------- | ------------ | --------- |
| ORDER | ZOO_ANIMAL         |             |         | an_nom   | an_espece    | an_classe |
| DOC   | ZOO_ANIMAL         | aliRotor    |         | Rotor    | ZOO_ESP_ALLI | Reptilia  |
| DOC   | ZOO_ANIMAL         | 2079        |         | Théodor  | ZOO_ESP_ALLI | Reptilia  |
| DOC   | ZOO_ANIMAL         | 2080        |         | Éléonore | ZOO_ESP_ALLI | Reptilia  |

L'option _avec les fichiers_ indique que l'exportation générera un fichier
archive de type Zip. Cette archive contiendra le fichier `fdl.csv` qui contient
les valeurs des attributs et les fichiers attachées aux documents exportés.
Cette archive peut être réimporté à l'[importation d'archive][importArchive].
Pour des raisons de compatibilité avec les différents systèmes d'exploitations
les noms des fichiers exportés ne comportent pas d'accents

### Données brutes {#core-ref:2e22b0a8-5148-4f74-8cc8-e56baae42c7e}

Le fichier produit est un fichier _csv_. ce fichier n'est pas réimportable.
Il ne contient que les valeurs brutes d'attributs.

    
|   nom    |    espèce    |   classe  |
| -------- | ------------ | --------- |
| Rotor    | ZOO_ESP_ALLI | Reptilia  |
| Théodor  | ZOO_ESP_ALLI | Reptilia  |
| Éléonore | ZOO_ESP_ALLI | Reptilia  |

La première ligne contient les libellés des attributs exportés.

### Données formatées {#core-ref:538a9069-167f-43de-8a25-96d0dd5d70e9}

 Le fichier produit est un fichier _csv_. ce fichier n'est pas réimportable.
    Il ne contient que les valeurs formatées d'attributs.

    
|   nom    |   espèce  |  classe  |
| -------- | --------- | -------- |
| Rotor    | Alligator | Reptilia |
| Théodor  | Alligator | Reptilia |
| Éléonore | Alligator | Reptilia |

La première ligne contient les libellés des attributs exportés.


À la différence des données brutes, l'espèce contient le titre et non l'identifiant.
De même, les énumérés contiendront le libellé et non la clefs.
La valeur formatée exportée est celle rendue sur les interfaces web à l'exception 
des hyperliens.



### Données XML Zip {#core-ref:dff8dc78-0ab8-481d-9e44-3a5cb0de2c61}

Chaque document est enregistré dans un fichier XML. Ces fichiers sont insérés dans 
un fichier d'[archive Zip][exportxmlzip]. 

### Données XML simple {#core-ref:f600301c-c2c3-4097-a4d7-1e57b8477dbc}

Chaque document est enregistré dans un seul et même [fichier XML][exportxml]. 

<!-- links -->
[ImportationCSV]: #core-ref:2fb3284a-2424-44b2-93ae-41dc3969e093
[importArchive]: #core-ref:021b7db1-7baf-48c4-8eb9-4a388355dd86
[attrfile]:  #core-ref:0e904376-317c-426e-bc6d-e56fd52bad89
[attrimage]: #core-ref:4fca7712-59e0-4186-bfd0-6214104a0f60
[exportxmlzip]: #core-ref:1b0958b2-0788-45bf-974a-a7853a6030e2 "détail format exportation archive XML"
[exportxml]: #core-ref:9cebde3e-d40c-421c-85f6-e3e8282d547f "détail format exportation XML"
[exportprofil]: #core-ref:602c6331-7cdb-4b24-8a56-ffd11e00502f
