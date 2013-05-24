# Importation d'archive {#core-ref:021b7db1-7baf-48c4-8eb9-4a388355dd86}
 
Ce chapitre décrit comment il est possible d'importer des documents avec des
fichiers liés aux documents.

## Importation de fichiers brute {#core-ref:05c1349e-a032-40e3-9a32-e48a14a2cd97}

Une archive brute permet d'importer un ensemble de fichiers. Ces fichiers seront
inclus dans des familles qui ont au moins un attribut de type _[file][attrfile]_
ou _[image][attrimage]_.

L'association entre la famille et le fichier est la suivante :

*   Fichier image : Famille _Image_ `IMAGE`
*   Autre fichier : Famille _Fichiers_ `FILE`
*   Répertoire : Famille _Dossier_ `DIR`

L'éventuelle arborescence du contenu de l'archive est conservé.


        $ unzip -l Files.zip
        Archive:  Files.zip
          Length      Date    Time    Name
        ---------  ---------- -----   ----
                0  2012-08-30 16:19   Dossier un/
             1321  2012-08-30 16:19   Dossier un/design.odt
             3321  2012-08-30 16:19   Dossier un/presentation.odp
                0  2009-02-26 16:07   Dossier deux/
           152726  2007-07-06 10:36   Dossier deux/notes techniques.doc
            63728  2007-07-06 10:36   Dossier deux/architecture.png

Cet extrait d'archive va créer deux dossiers, 3 documents de la famille
_fichiers_ et un document de la famille _image_.

Les fichiers sont insérés dans le premier attribut _fichier_ trouvé de la
famille associée.

## Importation d'archive {#core-ref:ffa26749-fd4a-497a-9b78-6a86e3e0a5e0}

Pour associer plus précisément les fichiers et les documents, il est nécessaire
d'indiquer ces relations dans un fichier `fdl.csv` qui est un format CSV
d'[importation de document][importcsv].

Si ce fichier est présent à la racine de l'archive, alors **seul ce fichier**
sera importé. Les autres fichiers servent dans ce cas à enregistrer les fichiers
qui sont indiqués dans le fichier `fdl.csv`.

| //FAM | animal(ZOO_ANIMAL) | Identifiant | Dossier |   nom    |    espèce    |                 photo                  |
| ----- | ------------------ | ----------- | ------- | -------- | ------------ | -------------------------------------- |
| ORDER | ZOO_ANIMAL         |             |         | an_nom   | an_espece    | an_photo                               |
| DOC   | ZOO_ANIMAL         | aliRotor    |         | Rotor    | ZOO_ESP_ALLI | Photos/1387_IMG_1684AFC2.jpg           |
| DOC   | ZOO_ANIMAL         |             |         | Théodor  | ZOO_ESP_ALLI | Photos/250px-Alligator.jpg             |
| DOC   | ZOO_ANIMAL         |             |         | Éléonore | ZOO_ESP_ALLI | Photos/alligator-9112.jpg              |
| DOC   | ZOO_ANIMAL         |             |         | Gator    | ZOO_ESP_ALLI | Images/Gator.png                       |
| DOC   | ZOO_ANIMAL         |             |         | Olgator  | ZOO_ESP_ALLI | Images/Reptilia_American_alligator.jpg |

Dans cet exemple les chemins des fichiers devant être insérés dans l'attribut
`an_photo` sont indiqués. Les fichiers devront être présents dans l'archive pour
être intégrés dans le document.

Cela donne une archive telle que celle-ci :

    $ unzip -l Animals.zip
    Archive:  Animals.zip
      Length      Date    Time    Name
    ---------  ---------- -----   ----
         1205  2012-08-30 16:19   fdl.csv
            0  2012-08-30 16:19   Photos/
        12689  2012-08-30 16:19   Photos/1387_IMG_1684AFC2.jpg
        11321  2012-08-30 16:19   Photos/250px-Alligator.jpg
        21521  2012-08-30 16:19   Photos/alligator-9112.jpg
            0  2009-02-26 16:07   Images/
        83728  2007-07-06 10:36   Images/Gator.png 
       163728  2007-07-06 10:36   Images/Reptilia_American_alligator.jpg



## Commande d'importation d'archive {#core-ref:fbd78f4f-9c6c-46ab-8218-b1dc2527d919}

La commande à lancer en console est :

    ./wsh.php --api=importDocuments --archive=yes --file=animals.zip

**Note** : L'option `--archive=yes` doit être indiqué pour ne pas confondre 
   avec une importation classique de fichier CSV ou XML.

Le format d'archive peut être [zip][zip] ou [tgz][tgz].

<!-- links -->
[mimetype]: http://fr.wikipedia.org/wiki/Type_MIME "Type mime sur wikipedia"
[attrfile]:  #core-ref:0e904376-317c-426e-bc6d-e56fd52bad89
[attrimage]: #core-ref:4fca7712-59e0-4186-bfd0-6214104a0f60
[zip]: http://fr.wikipedia.org/wiki/ZIP_%28format_de_fichier%29 "format ZIP sur Wikipedia"
[tgz]: http://fr.wikipedia.org/wiki/Tgz "Tar compressé sur Wikipedia"
[importcsv]: #core-ref:2fb3284a-2424-44b2-93ae-41dc3969e093