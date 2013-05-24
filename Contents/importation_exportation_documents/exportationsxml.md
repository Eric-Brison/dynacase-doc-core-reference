# Exportation de documents en _Xml_ {#core-ref:4d098747-0120-4ead-b13e-97ef1250e08d}

Les documents, hormis les familles, peuvent être exportés en XML. Les fichiers
XML produits suivent un schéma de famille imposé par dynacase. Chaque famille de
document a son propre schéma XML. L'exportation _Xml_ d'un contenu de dossier ou
de recherche peut se faire de deux façons : en générant un fichier par document
ou avec un seul fichier xml.

Si vous voulez utiliser le fichier _Xml_ pour un exportation vers un autre
contexte dynacase, il faut indiquer l'option "sans les identificateurs", sinon
les documents importés seront considérés comme des mises à jours.

Les fichiers produits par l'exportation _Xml_ sont conformes au format
d'[importation XML][importXML].

## Archive avec un fichier _Xml_ par document {#core-ref:1b0958b2-0788-45bf-974a-a7853a6030e2}

Dans ce cas une archive (zip) est constituée avec un fichier par document.
Chaque fichier est nommé à l'aide du titre et de l'identifiant du document (ex
:`alligator {4567].xml`). Chaque fichier fait référence à un [schéma
xml][xmlschema] issus de la famille. Ce schéma est aussi présent dans l'archive.

## Un fichier _Xml_ seul {#core-ref:9cebde3e-d40c-421c-85f6-e3e8282d547f}

Dans ce cas, la sortie est un seul fichier _xml_ contenant l'ensemble des
documents. La balise racine est dans ce cas `documents`. La balise documents
porte la date de génération et l'auteur.

    [xml]
    <documents date="2010-06-07T12:46:45"
    author="Default Master"
    name="recherche_animal">
        <zoo_animal .> </zoo_animal>
        <zoo_animal .> </zoo_animal>
    </documents>

Avec cette option les schémas _Xml_ des familles ne sont pas exportés.

## Exemple d'un document exporté {#core-ref:f0d2fdee-efd0-4c31-937b-b29b7a5da5d2}

    [xml]
    <zoo_animal xsi:noNamespaceSchemaLocation="zoo_animal.xsd" id="3296" name=""
        title="Alli Alligator" revision="0" modification-date="2010-06-02T13:53:33"
        version="" state="">
        <an_tab1>
            <an_identification>
                <an_nom>Alli</an_nom>
                <an_descr xsi:nil="true"/>
                <an_tatouage xsi:nil="true"/>
                <an_espece_title>Alligator</an_espece_title>
                <an_espece id="1127">Alligator</an_espece>
                <an_ordre>Crocodiliens</an_ordre>
                <an_classe id="1123" name="Reptilia">Reptilia</an_classe>
                <an_sexe>M</an_sexe>
                <an_photo xsi:nil="true"/>
                <an_photo vid="27" mime="image/png" href="http://localhost:8080/dev/file/3296/743/an_photo/-1/Gator.png?cache=no&amp;inline=no" title="alligator.png"/>
                <an_naissance>2010-05-12</an_naissance>
                <an_entree>2010-05-18</an_entree>
                <an_pere id="1289">Viel Ali Alligator</an_pere>
            </an_identification>
        </an_tab1>
    </zoo_animal>

## Exportation _Xml_ avec fichier {#core-ref:b81787b0-8fca-4f05-97e6-dd163b3fc2aa}

Si vous cochez l'option avec les fichiers ceux-ci seront importés "inline" dans les fichiers xml. La balise de l'attribut
contiendra dans ce cas le fichier encodé en base 64.

    [xml]
    <an_photo vid="27" mime="image/png" title="alligator.png">
    iVBORw0KGgoAAAANSUhEUgAAAQAAAAEACAYAAABccqhmAAAACXBIWXMAAAsTAAALEwEAmpwYAAAABGdBTUE
    AALGOfPtRkwAAACBjSFJNAAB6JQAAgIMAAPn/AACA6QAAdTAAAOpgAAA6mAAAF2+SX8VGAAEoA0lEQVR42m
    L8//8/wwgE==</an_photo>



## Exportation _Xml_ par ligne de commande {#core-ref:63238f3a-de09-45fa-b12b-854c569561c2}

L'exportation en ligne de commande est :

    ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=[folderid] --eformat=[X|Y] --wfile=[N|Y]

Les paramètres sont :

id
:   Identifiant d'un dossier ou d'une recherche

eformat
:   
    
    *   X : Archive XML
    *   Y : _Xml_ simple

wfile
:   
    
    *   Y : Avec fichiers
    *   N : Sans fichier

Exportation _Xml_ sans fichier
:   

        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=Y > t.xml

Exportation _Xml_ avec fichier
:   

        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=Y --wfile=Y> t.xml

Exportation Zip sans fichier
:   

        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=X > t.zip

Exportation Zip avec fichier
:   

        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=X --wfile=Y> t.zip

Exportation _Xml_ avec option flat pour une mise à plat des attributs. 
:   Ce type d'exportation ne permet pas une réimportation
dans dynacase. Les balises de structure de type "tab" et "frame" ne sont pas représentées. Seules la structure
concernant les tableaux est maintenu.
    
        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=Y --flat=Y> t.xml

Exportation _Xml_ avec log. 
: Cette option permet de connaître le nombre de documents exportées ainsi que la liste de ceux-
ci.
    
        ./wsh.php --app=FDL --action=EXPORTXMLFLD --id=1180 --eformat=Y --log=/var/tmp/log.txt > t.xml
        ~$ more /var/tmp/log.txt
        EXPORT BEGIN OK : 02/07/2010 15:49:47
        EXPORT OPTION FLAT : no
        EXPORT OPTION WFILE : yes
        EXPORT OPTION CONFIG : yes
        EXPORT OPTION ID : ANIMAUX <Les animaux>
        EXPORT DOC OK : <a Agouti> [3300]
        EXPORT DOC OK : <Albert baleine blanche> [3266]
        EXPORT DOC OK : <Alli Baleine à bosse ou jubarte> [3248]
        EXPORT DOC OK : <Zoé Antilope> [3317]
        EXPORT COUNT OK : 3
        EXPORT END OK : 02/07/2010 15:49:47

Exportation _Xml_ avec spécification des attributs à exporter. 
:   Cela est paramétrable à l'aide d'un fichier de configuration xml


Exemple :

    [xml]
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <family name="ZOO_ANIMAL">
            <attribute name="AN_NOM"/>
            <attribute name="AN_ESPECE"/>
            <attribute name="AN_ENFANT"/>
        </family>
            <family name="ZOO_ENCLOS">
            <attribute name="EN_NOM"/>
            <attribute name="EN_SURFACE"/>
        </family>
    </configuration>

Chaque balise `family` défini les attributs qu'il veut voir apparaître. Seuls
les attributs "feuille" non structurants sont pris en compte. Les attributs `name`
désignent les identifiants de familles et d'attributs. Si on exporte un document
d'une famille qui n'est pas dans le fichier de configuration, l'ensemble de ses
attributs sera exporté.

    ./wsh.php --app=FDL --action=EXPORTXMLFLD --flat=no --id=ANIMAUX --wfile=yes
        --eformat=Y --config=configexport.xml --log=/var/tmp/log.txt > animaux.xml


<!-- links -->
[xmlschema]: http://fr.wikipedia.org/wiki/XML_Schema
[importXML]: #core-ref:81ad5a48-4c0f-468b-90ed-fe462fba7b96