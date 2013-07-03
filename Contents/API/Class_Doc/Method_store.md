# Doc::store() {#core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12}

<div class="short-description">
Cette méthode enregistre les modifications d'un document en base de données.
</div>



## Description {#core-ref:cc7830a4-96e4-4e35-8980-8224905b815d}

    [php]
    <string> store (&$info = null, $skipConstraint = false )

Cette méthode permet la modification ou la création de document. Si le document
n'a pas d'identifiant (`id`), une création de document sera effectuée, sinon le
document sera mis à jour.

### Avertissements {#core-ref:fd0141dc-9206-4ce8-8aca-e4908c64a3f4}

Aucun.

## Liste des paramètres {#core-ref:7b480a74-4e45-41ff-8d0a-c15f503feb61}

[out] (storeInfo) `info`
:   Si `info` est fourni, il contiendra les différents messages fournis par les
    hameçons ainsi que le code d'erreur.

[in] (bool) `skipConstraint`
:   Si la valeur est `false` alors les [contraintes][contraintes] sur le 
    document ne sont pas testés.


## Valeur de retour {#core-ref:220144a4-6c58-4480-8247-3dbec4d23913}

La valeur de retour contient le message d'erreur.
Si l'enregistrement s'est bien passé le retour est une chaine de caractère vide.
Dans le cas contraire, le texte de l'erreur est retourné.

Des informations plus détaillées sont disponibles dans le paramètre `$info`.

## Erreurs / Exceptions {#core-ref:8b5b15c4-851b-4a34-9fa7-7ce5d1db8bd4}

Si la création ou la modification n'a pas pu être réalisée, alors la méthode
retourne un message d'erreur.

Code retour de `$info` : storeInfo::errorCode :

storeInfo::NO_ERROR
:   Pas d'erreur.

storeInfo::CREATE_ERROR
:   Erreur lors de la création. Peut provenir de l'hameçon 
    `Doc::preCreated()`, d'un problème de droits ou d'un problème d'accès à
    la base de données.

storeInfo::UPDATE_ERROR
:   Erreur lors de la mise à jour.  Peut provenir d'un problème de droits 
    ou d'un problème d'accès à la base de données.

storeInfo::CONSTRAINT_ERROR
:   Une des contraintes n'a pas été validée.

storeInfo::PRESTORE_ERROR
:   Erreur déclenchée par l'hameçon `Doc::preStore()`.

Une exception `Dcp\Db\Exception` peut être levée en cas de problème
d'enregistrement au niveau de la base de données (problème d'accès, problème de
unicité d'index, problème d'incohérence de type).

## Historique {#core-ref:cb88c9b8-25d8-4f7e-9147-e7e54509f813}

Aucun.

## Exemples {#core-ref:16fe9687-083a-4dae-9f71-efb291500a03}

Soit la famille MY_FAMILY suivante :


| BEGIN |                   |     Ma famille    |                |     | MYFAMILY |       |     |     |
| ----- | ----------------- | ----------------- | -------------- | --- | -------- | ----- | --- | --- |
| CLASS | My\MyFamily       |                   |                |     |          |       |     |     |
| //    | idattr            | idframe           | label          | T   | A        | type  | ord | vis |
| ATTR  | MY_IDENTIFICATION |                   | Identification | N   | N        | frame | 10  | W   |
| ATTR  | MY_NUMBERONE      | MY_IDENTIFICATION | nombre 1       | Y   | N        | int   | 20  | W   |
| ATTR  | MY_NUMBERTWO      | MY_IDENTIFICATION | nombre 2       | N   | N        | int   | 30  | W   |
| END   |                   |                   |                |     |          |       |     |     |


### Modification d'un document 

Exemple d'enregistrement d'une modification sans contrôle d'erreur.

    [php]
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    /** @var \Dcp\Family\MyFamily */
    $d=new_Doc("","MY_DOCUMENT");
    $d->setValue(Aself::my_numberone, 234);
    $d->store($info); // enregistrement en base de données


### Création d'un document 

Exemple d'enregistrement d'un nouveau document sans contrôle d'erreur.

    [php]
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    /** @var \Dcp\Family\MyFamily */
    $d=createDoc("","MY_FAMILY");
    $d->setValue(Aself::my_numberone, 234);
    $d->setValue(Aself::my_numbertwo, 873);
    $d->store($info);// enregistrement en base de données
    printf("Nouvel identifiant : %d\n", $d->id);

### Contrôle des erreurs d'enregistrement

Les codes erreurs de `$info` permettent de préciser l'origine du problème.

    [php]
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    /** @var \Dcp\Family\MyFamily */
    $d = new_Doc("", "MY_DOCUMENT");
    $err = $d->setValue(Aself::my_numberone, 234);
    
    if (empty($err)) {
        /** @var storeInfo $info */
        $err = $d->store($info);
        if (!empty($err)) {
            switch ($info->errorCode) {
                case storeInfo::NO_ERROR:
                    // pas d'erreurs
                    break;
                case storeInfo::CONSTRAINT_ERROR:
                    printf("Erreurs de contrainte :\n");
                    foreach ($info->constraint as $constraintInfo) {
                        printf("Contrainte sur l'attribut %s non respectée : %s\n", 
                            $constraintInfo["id"], 
                            $constraintInfo["err"]);
                    }
                    break;
                default:
                    printf("Erreur d'enregistrement : %s", $err);
            }
        }
    }

## Notes {#core-ref:86dea093-c4a0-4c98-b47b-73fa0221ec30}

Lors d'un ajout de documents les hameçons suivants sont lancés :

1.  [`Doc::preStore()`][docprestore]
1.  [`Doc::preCreated()`][docprecreated]  
    Enregistrement en base
1.  [`Doc::postCreated()`][docpostcreated]
1.  [`Doc::preRefresh()`][docprerefresh]
1.  [`Doc::postRefresh()`][docpostrefresh]  
    Enregistrement en base si modification détectée depuis dernier enregistrement
1.  [`Doc::postStore()`][docpoststore]  
    Enregistrement en base si modification détectée depuis dernier enregistrement

Lors d'une mise à jour de documents les hameçons suivants sont lancés :


1.  [`Doc::preStore()`][docprestore]
1.  [`Doc::preRefresh()`][docprerefresh]
1.  [`Doc::postRefresh()`][docpostrefresh]  
    Enregistrement en base
1.  [`Doc::postStore()`][docpoststore]  
    Enregistrement en base si modification détectée depuis dernier enregistrement

## Voir aussi {#core-ref:9e1551ac-c4d3-41ab-bc19-4bb641db900f}

*   [Doc::setAttributeValue][docsetattrvalue]
*   [Doc::setValue][docsetvalue]

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpostcreated]:   #core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45 "Hameçon Doc::postCreated()"
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docprestore]:      #core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0 "Hameçon Doc::preStore()"
[docprecreated]:    #core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747 "Hameçon Doc::preCreated()"
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[contraintes]:      #core-ref:7b41906b-f199-41a4-94df-33b9ad34153b
[docaddrevision]:   #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38
[docsetvalue]:      #core-ref:febc397f-e629-4d47-955d-27cab8f4ed2f
[docsetattrvalue]:  #core-ref:1e766800-b2e1-462b-9793-b0261ede8677