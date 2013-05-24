# Importer des documents par ligne de commande {#core-ref:1c97f553-dcba-454e-96a0-8059230065b3}

La commande _wsh_ `importDocuments` permet d'importer des documents en ligne de commande. Les types CVS, ODS, XML, ZIP, TGZ (pour les archives)  sont supportés par le script :

    ./wsh.php --api=importDocuments --file=/home/dev/Bureau/animals.csv

    Import documents from description file
    Usage :
        --file=<the description file path>
       Options:
        --userid=<user system id or login name to execute function - default is (admin)>, default is '1'
        --analyze=<analyze only> [yes|no], default is 'no'
        --archive=<description file is an standard archive (not xml)> [yes|no], default is 'no'
        --log=<log file output>
        --policy=<policy import - 
            [update] to auto update same document (the default), 
            [add] to always create new document, 
            [keep] to do nothing if same document already present> [update|add|keep]
        --htmlmode=<analyze report mode in html> [yes|no], default is 'yes'
        --reinitattr=<reset attribute before import family update> [yes|no]
        --to=<email address to send report>
        --dir=<folder where imported documents are put>
        --strict=<don't import if one error detected> [yes|no], default is 'yes'
        --help (Show usage) 

    

Pour réaliser une importation à blanc, l'option _analyze_ doit être à _yes_. Dans
ce cas, l'importation est réalisée mais modification n'est enregistrée en base
de données :

     ./wsh.php --api=importDocuments --analyze=yes --htmlmode=yes --file=animal.xml > report.html

Pour envoyer le rapport par courriel, l'option _to__ doit avoir l'adresse du
destinataire

     ./wsh.php --api=importDocuments --to=someone@somewhere.org --file=animal.xml 

Pour avoir un fichier de log, l'option _log_ doit contenir l'endroit où le
fichier de log sera enregistré

    ./wsh.php --api= importDocuments --file=animaux.xml --htmlmode=yes --analyze=yes --log=/var/tmp/log.txt
    $ cat /var/tmp/log.txt
    IMPORT BEGIN OK : 02/07/2010 17:10:29
    IMPORT DOC OK : [title:Isabelle] [id:0] [action:added] [changes:{nom:Isabelle}{espèce:1132}] [message:Isabelle à ajouter] 
    IMPORT DOC OK : [title:Alli2 Agouti] [id:3296] [action:updated] [changes:] [message:]
    IMPORT DOC KO : [title:] [id:0] [action:ignored] [changes:] [message:] [error:DOMDocument::load(): Opening and ending tag mismatch: r line 5 and zoo_animal in /var/tmp/xmlsplit4c2e10009374f/3299.xml, line: 10DOMDocument::load(): Premature end of data in tag zoo_animal line 2 in /var/tmp/xmlsplit4c2e10009374f/3299.xml, line: 11]
    IMPORT COUNT OK : 2
    IMPORT COUNT KO : 1
    IMPORT END OK : 02/07/2010 17:10:31

Si une seule erreur est détectée sur le fichier d'importation, aucun document du fichier d'importation ne sera ajouté ou modifié.

<!-- links -->