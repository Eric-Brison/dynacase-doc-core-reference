# Doc::preStore()  {#core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0}

<div class="short-description" markdown="1">
Hameçon utilisé par la méthode [`Doc::Store()`][docstore]. Elle est appelée
avant l'enregistrement en base de données. Cette méthode doit vérifier si les
conditions de modification de document sont valides.

</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description  {#core-ref:6a386ab6-e2c9-419e-a8c7-7875df6c2db8}

    [php]
    <string> preStore ()

Si cette méthode retourne un message d'erreur alors la modification sera
abandonnée et la méthode `Doc::store()` retournera le message fournie par cette
méthode afin d'indiquer l'échec.


### Avertissements  {#core-ref:c3c55aac-e6fb-49f1-b62c-16e57ab8d984}

Le document n'a pas encore d'identificateur lors d'une création.
Cette méthode n'est pas appelée lors d'une révision.

## Liste des paramètres  {#core-ref:63a1e5c8-731a-40b9-b1b3-54dec73995ea}

Aucun paramètre.

## Valeur de retour  {#core-ref:b6b77dad-14f4-47da-994f-ec8719f01563}

Message d'erreur. Si la méthode retourne une chaîne de caractère non vide, elle
sera considérée comme un message d'erreur et la création de document sera
abandonnée.

Ce message est aussi stocké dans le paramètre de sortie `$info->preStore` de la
méthode `Doc::store()`.

## Erreurs / Exceptions  {#core-ref:3689ef07-59b4-4b63-9763-48d7f6d2565b}

Aucune.

## Historique  {#core-ref:1988b945-7432-48f3-8b55-10eb16d9be00}

Aucun.

## Exemples  {#core-ref:2628e1ce-7af9-41dc-acae-0e009091357d}

Dans la famille _MyFamily_, la modification d'un document ne devra être
possible que si la somme des attributs MY_NUMBERONE et MY_NUMBERTWO est
supérieur au paramètre MY_MAX de la famille.

Soit la famille suivante :

| BEGIN |                   |     Ma famille    |                |     | MYFAMILY |       |     |     |
| ----- | ----------------- | ----------------- | -------------- | --- | -------- | ----- | --- | --- |
| CLASS | My\MyFamily       |                   |                |     |          |       |     |     |
| //    | idattr            | idframe           | label          | T   | A        | type  | ord | vis |
| ATTR  | MY_IDENTIFICATION |                   | Identification | N   | N        | frame | 10  | W   |
| ATTR  | MY_NUMBERONE      | MY_IDENTIFICATION | nombre 1       | Y   | N        | int   | 20  | W   |
| ATTR  | MY_NUMBERTWO      | MY_IDENTIFICATION | nombre 2       | N   | N        | int   | 30  | W   |
| PARAM | MY_PARAMETERS     |                   | Paramètres     | N   | N        | frame | 10  | W   |
| PARAM | MY_MAX            | MY_PARAMETERS     | max            | N   | N        | int   | 20  | W   |
| END   |                   |                   |                |     |          |       |     |     |


    [php]
    namespace My;
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    class MyFamily extends \Dcp\Family\Document
    {
        public function preStore()
        {
            $err = '';
            $n1 = $this->getAttributeValue(Aself::my_numberone);
            $n2 = $this->getAttributeValue(Aself::my_numbertwo);
            $max = $this->getFamilyParameterValue(Aself::my_max);
            if (($n1 + $n2) > $max) {
                $err = sprintf("Max %d is reached", $max);
            }
            return $err;
        }
    }

## Notes  {#core-ref:1815fc08-a3a7-4a80-8c37-9a0487bcf2ba}

En cas de famille héritée, il est nécessaire d'appeler l'hameçon du parent pour
disposer des mêmes fonctionnalités.

## Voir aussi  {#core-ref:4d2d6173-d571-4f45-89e5-aa2f9dea64d9}

*   [Doc::store][docstore]
*   [Doc::preCreated][docprecreated]
*   [Doc::postCreated][docpostcreated]
*   [Doc::preCreated][docprecreated]
*   [Doc::preStore][docprestore]

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpostcreated]:   #core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45 "Hameçon Doc::postCreated()"
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docprestore]:      #core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0 "Hameçon Doc::preStore()"
[docprecreated]:    #core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747 "Hameçon Doc::preCreated()"
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrevise]:        #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38