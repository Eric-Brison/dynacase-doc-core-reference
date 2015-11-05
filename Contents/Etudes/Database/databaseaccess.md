# Accès à la base de données {#core-ref:94b8faba-5195-4250-bb85-339f478f7961}

L'accès à la base donnée est défini à l'aide d'un [service
Postgresql][pgservice].

Les coordonnées du service sont obtenues avec la fonction `getDbAccess()`.

    [php]
    $dbAccess = getDbAccess();
    printf("Database [%s]\n",$dbAccess);

Résultat :

    Database [service='developpement']

L'accès peut être réalisé avec la fonction PHP [`pg_connect`][pgconnect].

    [php]
    $resource = pg_connect($dbAccess);
    var_dump($resource);

Résultat :

    resource(26) of type (pgsql link)

Les classes héritées de [DbObj][dbobj], notamment la classe [`Doc`][docclass],
utilisent une abstraction qui permet de [gérer][dbobjapi] l'accès et
l'enregistrement des données en base.

L'accès à la base de données de manière explicite est à réserver pour des
besoins spécifiques. La manipulation des documents et autres objets de Dynacase
doit être fait à travers leurs classes PHP respectives.

<!-- links -->

[pgservice]:     http://www.postgresql.org/docs/9.1/static/libpq-pgservice.html "PostgreSql Service"
[dbobj]:        #core-ref:1e07e79d-3760-4d8b-9e41-95c3fb63af08
[dbobjapi]:     #core-ref:7a62bb83-17a0-478d-a853-bc359d0fb8fb
[docclass]:     #core-ref:1d557fb4-4eca-4ab8-a334-974fe563ddd2
[pgconnect]:    http://www.php.net/manual/fr/function.pg-connect.php "pg_connect sur php.net"