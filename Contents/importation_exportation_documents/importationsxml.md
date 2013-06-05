# Importation de documents par XML {#core-ref:81ad5a48-4c0f-468b-90ed-fe462fba7b96}
 
Ce chapitre indique comment importer des documents au format XML.

L'importation de document peut être faite à l'aide de fichiers XML tels que ceux
produits par l'exportation XML.

Le type de fichier accepté est soit un fichiers XML avec la balise root
`<documents>`, soit un fichier archive `zip` contenant un ensemble de
fichiers XML. Ces fichiers XML doivent être conformes au schéma XML associé à la
famille de document.

## Schéma XML d'une famille {#core-ref:d28f9655-2db3-4073-a8bf-cb1edd89ed8d}

<span class="fixme" data-assignedto="EBR">on met les IHMs?</span>
Le schéma d'une famille est accessible depuis le _centre d'administration_.
Dans l'application `Explorateur de documents`, le menu `Outils/Importer des
documents` ouvre l'interface d'importation de documents. Le bouton _Récupérer le
schéma XML_ permet de télécharger le `.xsd` correspondant à la famille
sélectionnée.

En ligne de commande, l'action `FDL:FDL_FAMILYSCHEMA` permet de récupérer ce
[schéma XML][xmlschema]. L'argument `id` doit contenir l'identifiant de la
famille dont on veut le schéma.

    ./wsh.php --app=FDL --action=FDL_FAMILYSCHEMA --id=ZOO_ANIMAL > zoo_animal.xsd

Les fichiers XML peuvent être validés à l'aide du schéma avant importation.
Cette vérification est à faire manuellement à l'aide du schéma correspondant.
Le logiciel _[xmllint][xmllint]_ permet de vérifier vos fichiers XML.<span
class="fixme" data-assignedto="EBR">ce n'est pas à nous d'expliquer comment on
se sert d'un schéma…</span>

          
    $ xmllint --noout --schema zoo_animal.xsd  myanimal.xml
    

## Relation  {#core-ref:46f5af7a-46c8-43b8-a2df-a89ea89aea75}

Pour déclarer une relation avec un autre document, l'attribut `name` permet
d'indiquer la référence (nom logique) du document lié.

    [xml]
    <an_classe name="Reptilia">Reptile</an_classe>

L'attribut `id` permet d'indiquer la référence système (numérique). Ceci ne peut
fonctionner que sur une base de données identifiée car les références systèmes
varient d'une base à une autre.

    [xml]
    <an_espece id="4563">Alligator</an_espece>

Si ni l'attribut `name` ni l'attribut `id` n'est indiqué, une recherche par
titre sera faite afin de trouver automatiquement le document qui a le même titre
en cohérence avec la famille déclarée dans la relation au niveau de la famille.
Si aucun identifiant n'est trouvé la valeur de l'attribut sera vide.<span
class="fixme" data-assignedto="EBR">pas de notice ou de warning?</span>

    [xml]
    <an_espece>Alligator</an_espece>


## Fichier _inline_ {#core-ref:e9a0454c-5f1a-4eb1-b499-12f5c4efe52e}

Des fichiers peuvent être enregistrés pour les attributs de type
[file][attrfile] ou [image][attrimage]. 

Les fichiers encodés contenus dans le XML sont insérés dans le document et
remplace le fichier original. Le contenu du fichier doit être encodé en
[base64][base64].

    [xml]
    <zoo_animal xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="zoo_animal.xsd" name="aliRotor" title="Rotor" > 
      <an_identification><an_nom>Rotor</an_nom>
      <an_tatouage xsi:nil="true"/>
      <an_espece name="ZOO_ESP_ALLI">Alligator</an_espece
      <an_ordre>Crocodiliens</an_ordre>
      <an_classe name="Reptilia">Reptilia</an_classe>
      <an_sexe>M</an_sexe>
      <an_photo  mime="image/jpeg; charset=binary" title="1387_IMG_1684AFC2.jpg">/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFxQYGBcUFhYaHSUfGhsjHBYWICwgIyYnKSopGR8tMC0oMCUoKSj/2wBDAQcHBwoIChMKChMoGhYaKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgQFFAH/9k=</an_photo>
      <an_gardien xsi:nil="true"/>
      <an_naissance>2012-08-03</an_naissance>
      <an_entree xsi:nil="true"/>
      <an_pere>Théodor</an_pere>
      <an_mere>Éléonore</an_mere>
      </an_identification>
    </zoo_animal>

Dans cet exemple la balise `an_pĥoto` contient l'image. L'attribut `title`
contient le nom du fichier. S'il est vide, le nom du fichier sera `noname`.
L'attribut `mime` est obligatoire, il contient le [typemime][mimetype] du
fichier attaché.

## Entêtes des fichiers XML {#core-ref:9a6352fe-8882-4580-837a-bc42380bb617}

L'entête d'un document importé en XML contient les informations suivantes :

    [xml]
    <zoo_animal 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="zoo_animal.xsd" 
       title="Babette Junior"
       revision="1"
       modification-date="2012-08-01T09:51:14"
       version="" state="alive">


Les attributs `title`, `revision`, `modification-date`, `version` présents lors
d'une exportation XML sont calculés.  Ils sont ignorés lors de l'importation.

De même l'attribut *state* n'est pas pris en compte.  En revanche, les valeurs
de ces attributs sont disponibles en [informations complémentaires][extra] dans
les méthodes `::preImport()` et `::postImport()` pour réaliser un traitement
particulier.

Les attributs optionnels `id`, `name`, `folders`  sont pris en compte lors de
l'importation.

name
:   Indique l'identifiant logique d'un document.
    
    L'utilisation de cette propriété indique qu'on va créer un document avec ce
    nom logique ou mettre à jour le document portant ce nom logique.

folders
:   Indique les noms logiques des dossiers dans lesquels le document doit être
    inséré.
    
    S'il y a plusieurs dossiers, il faut séparer les noms par des virgules.

id
:   Indique l'identifiant système d'un document.
    
    L'utilisation de cette propriété indique qu'on va créer ou mettre à jour le
    document portant cet identifiant.
    
    En son absence, la base génère un nouvel identifiant.
    
    **Attention** : cet identifiant est propre à une base, et ne peut
    qu'exceptionnellement être utilisé d'une base à l'autre.

## Clefs d'importation XML {#core-ref:6a56e8e3-0e85-408f-a175-428818b1e0c0}

Avec la politique de mise à jour de document (par défaut), les documents sans
identifiants recherchent un document similaire avec les clefs d'importation. La
clef d'importation par défaut est `title`. Si un document et un seul de la même
famille avec le même titre a été trouvé alors il sera considéré comme une mise à
jour.

La clef d'importation peut être changée en utilisant l'attribut `key` :

    [xml]
    <zoo_animal xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
      xsi:noNamespaceSchemaLocation="zoo_animal.xsd"  key="an_tatouage" 
      revision="0" modification-date="2010-06-16T09:07:37" version="" state=""> 
      <an_identification>
         <an_nom>Gérard</an_nom>
         <an_espece id="1131">Antilope</an_espece>
         <an_tatouage>32</an_tatouage>
         <an_enfant_t><an_enfant id="1148">Totor Alligator</an_enfant></an_enfant_t>
         <an_enfant_t><an_enfant id="1147">Alli Alligator</an_enfant></an_enfant_t>
      </an_identification>
    </zoo_animal>

Dans cet exemple, ce sera le tatouage qui sera pris comme référence. Si un
animal de même tatouage est trouvé il sera mis à jour sinon il sera ajouté. Il
est possible d'avoir une clef secondaire en ajoutant après une virgule un
deuxième attribut : `key="an_tatouage,an_espece"`.

Cette directive est équivalente à la clef `KEYS` de [l'importation CSV][KEYS].

## Importer des documents avec un simple fichier XML  {#core-ref:bebebfa3-9b95-4884-a3e7-8b068100569f}

Le fichier XML à importer doit contenir l'ensemble des documents correspondants.
La balise principale est `documents`.

    animaux.xml

    [xml]
    <documents>
        <zoo_animal> 
          <an_identification>
             <an_nom>Gérard</an_nom>
             <an_espece id="1131">Alligator</an_espece>
             <an_tatouage>32</an_tatouage>
             <an_enfant_t><an_enfant id="1148">Totor Alligator</an_enfant></an_enfant_t>
             <an_enfant_t><an_enfant id="1147">Alli Alligator</an_enfant></an_enfant_t>
          </an_identification>
        </zoo_animal>
        <zoo_animal> 
          <an_identification>
             <an_nom>Bob</an_nom>
             <an_espece id="1134">Agouti</an_espece>
             <an_tatouage>31</an_tatouage>
          </an_identification>
        </zoo_animal>
    </documents>

La commande à lancer pour l'[importation en console][wshimport] est :

    ./wsh.php --api=importDocuments --file=animaux.xml

## Importer des documents en XML avec une archive {#core-ref:4aa6c12d-e98c-4f5e-b779-af667e29bddf}

### Structure de l'archive XML {#core-ref:8556e28c-7fdf-45b7-bb58-81080c7ae6ba}

La structure de l'archive doit contenir un ensemble de fichiers XML
correspondant chacun à un seul document. Chaque fichier est un XML qui est
conforme au [schéma XML][family_schema] de la famille. Les fichiers XML doivent
être placés uniquement à la racine de l'archive. Le format du fichier archive
pour l'importation XML est de type [zip][zip].

Exemple :

    $ unzip -l animals.zip 
    Archive:  animals.zip
      Length      Date    Time    Name
    ---------  ---------- -----   ----
          983  2013-05-29 10:19   Gator.xml
          947  2013-05-29 10:29   Olgator.xml
        15159  2013-05-29 09:59   zoo_animal.xsd
    ---------                     -------
        17089                     3 files

Cette archive contient deux documents. Le fichier schéma `zoo_animal.xsd` est
facultatif. Il est enregistré à titre indicatif pour pouvoir l'utiliser dans des
éditeurs XML. Il est ignoré lors de l'importation.


Validation des fichiers XML avant archivage : <span class="fixme" data-
assignedto="EBR">c'est pas à nous d'expliquer ça…</span>

    $ xmllint --noout --schema zoo_animal.xsd *xml
    Gator.xml validates
    Olgator.xml validates

Cette validation permet de vérifier que les fichiers sont corrects avant la
tentative d'importation.

La commande à lancer pour l'[importation en console][wshimport] est :

    ./wsh.php --api=importDocuments --file=animals.zip

**Note** : L'option `--archive=yes` n'est pas à utiliser dans ce cas. Elle est
réservée à l'[importation d'archive][importArchive].

### Insérer un fichier avec le format d'archive XML {#core-ref:60cfc982-ec27-4316-8e8c-d0f32bd1d194}

Les fichiers attachés peuvent être insérés _[inline][inlinefile]_ ou par
référence à un fichier local à l'archive.

Les fichiers à attacher doivent être insérés dans des sous-répertoires.

    $ unzip -l animals.zip 
    Archive:  animals.zip
      Length      Date    Time    Name
    ---------  ---------- -----   ----
            0  2013-05-29 10:27   Photos/
      2523262  2013-05-29 09:53   Photos/Gator.png
       168900  2013-05-29 10:27   Photos/Reptilia_American_alligator.jpg
          983  2013-05-29 10:19   Gator.xml
          947  2013-05-29 10:29   Olgator.xml
        15159  2013-05-29 09:59   zoo_animal.xsd
    ---------                     -------
      2709251                     6 files

Dans ce exemple, les deux photos à insérer dans les documents sont dans le
répertoire _Photos_.

    Gator.xml

    [xml]
    <?xml version="1.0" encoding="UTF-8"?>
    <zoo_animal xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >
      <an_identification>
        <an_nom>Gator</an_nom> 
        <an_tatouage xsi:nil="true"/>
        <an_espece name="ZOO_ESP_ALLI">Alligator</an_espece>
        <an_ordre>Crocodiliens</an_ordre>
        <an_classe name="Reptilia">Reptilia</an_classe>
        <an_sexe>F</an_sexe>
        <an_photo mime="image/png; charset=binary" href="Photos/Gator.png" title="Gator.png"/>
      </an_identification>
    </zoo_animal>

Le fichier lié doit être indiqué dans l'attribut XML `href` correspondant à la
balise de l'attribut fichier. Dans ce cas, il faut que la balise XML soit
autofermante, sinon cela sera considéré comme un fichier _inline_ et une erreur
d'importation se produira car le fichier _inline_ ne doit pas contenir
d'attribut `href`.

<!-- links -->
[KEYS]: #core-ref:7eefc8e7-16a6-4188-99d5-c2c9d817a1fe
[xmllint]: http://xmlsoft.org/xmllint.html
[base64]: http://fr.wikipedia.org/wiki/Base64
[importArchive]: #core-ref:021b7db1-7baf-48c4-8eb9-4a388355dd86
[inlinefile]: #core-ref:e9a0454c-5f1a-4eb1-b499-12f5c4efe52e
[mimetype]: http://fr.wikipedia.org/wiki/Type_MIME "Type mime sur Wikipédia"
[attrfile]:  #core-ref:0e904376-317c-426e-bc6d-e56fd52bad89
[attrimage]: #core-ref:4fca7712-59e0-4186-bfd0-6214104a0f60
[zip]: http://fr.wikipedia.org/wiki/ZIP_%28format_de_fichier%29 "format ZIP sur Wikipédia"
[xmlschema]: http://fr.wikipedia.org/wiki/XML_Schema "XML schema sur Wikipédia"
[wshimport]: #core-ref:1c97f553-dcba-454e-96a0-8059230065b3
[extra]: #core-ref:15088f40-de05-4600-86bb-82422af01dce
[family_schema]: #core-ref:d28f9655-2db3-4073-a8bf-cb1edd89ed8d
