# Doc::postCreated() {#core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45}

<div class="short-description" markdown="1">  

Hameçon utilisé par la méthode [`Doc::Store()`][docstore]`. Cette méthode est
appelé après l'enregistrement en base de données


</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description {#core-ref:bc70e39d-7ce2-4559-a6ae-99c48200e2e6}

    [php]
    <string> postCreated ()

Cette méthode est utilisable aussi pour réaliser un post-traitement après une
création de document. Elle ne peut pas annuler l'enregistrement. Le document
possède un identificateur est déjà enregistré en base.

Cette méthode est aussi appelée par `Doc::revise()` lorsque le document est
révisé. Une révision entraîne une création en base de données.

### Avertissements {#core-ref:49929040-b38d-4b2a-9432-98c48af2ff3a}

Il ne faut pas appeler la méthode Doc::store() dans cette méthode au risque
d'avoir une boucle infinie.

Si des modifications d'attributs sont réalisées dans cette méthode, ils seront
enregistrés en base par la méthode `Doc::store()`.

## Liste des paramètres {#core-ref:617d3a6d-a2b7-4288-b874-26c97e5e1307}

Aucun paramètre.

## Valeur de retour {#core-ref:355cb8b8-7c9f-41de-b573-0a204a2433f7}

La valeur de retour est un message d'information. Ce message sera enregistré
dans l'historique du document.

## Erreurs / Exceptions {#core-ref:24ecaa74-c05f-4808-ac16-c18bd44aa0d0}

Aucune.

## Historique {#core-ref:672081a6-eb13-429e-9957-dd6f591099f0}

Aucun.

## Exemples {#core-ref:7616c7bc-87bd-4e4e-9be8-e3ee70140c0d}

Dans la famille _MyFamily_, une référence unique est enregistré lors de la
création du document.

Soit la famille suivante :

| BEGIN |                   |     Ma famille    |                |     | MYFAMILY |       |     |     |
| ----- | ----------------- | ----------------- | -------------- | --- | -------- | ----- | --- | --- |
| CLASS | My\MyFamily       |                   |                |     |          |       |     |     |
| //    | idattr            | idframe           | label          | T   | A        | type  | ord | vis |
| ATTR  | MY_IDENTIFICATION |                   | Identification | N   | N        | frame | 10  | W   |
| ATTR  | MY_NUMBERONE      | MY_IDENTIFICATION | nombre 1       | Y   | N        | int   | 20  | W   |
| ATTR  | MY_NUMBERTWO      | MY_IDENTIFICATION | nombre 2       | N   | N        | int   | 30  | W   |
| ATTR  | MY_REF            | MY_IDENTIFICATION | Référence      | N   | N        | frame | 10  | R   |
| END   |                   |                   |                |     |          |       |     |     |


    [php]
    namespace My;
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    class MyFamily extends \Dcp\Family\Document
    {
        public function postCreated()
        {
            $msg = '';
            if ($this->revision == 0) { // création initiale
                $err = $this->setValue(Aself::my_ref, uniqid('my'));
                if ($err) {
                    $msg = sprintf("Pas d'identifiant");
                } else {
                    $msg = sprintf("Création identifiant %s", $this->getRawValue(Aself::my_ref));
                }
            }
            return $msg;
        }
    }



## Notes {#core-ref:a17763da-f5a3-480a-9a6e-8f901b767b53}

En cas de famille héritée, il est nécessaire d'appeler l'hameçon du parent pour
disposer des mêmes fonctionnalités.

## Voir aussi {#core-ref:fd05fb03-1114-4b6c-82c6-c44d311925e8}

*   [Doc::store][docstore]
*   [Doc::preCreated][docprecreated]
*   [Doc::preStore][docprestore]
*   [Doc::postStore][docpoststore]
*   [Doc::revise][docrevise]

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpostcreated]:   #core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45 "Hameçon Doc::postCreated()"
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docprestore]:      #core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0 "Hameçon Doc::preStore()"
[docprecreated]:    #core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747 "Hameçon Doc::preCreated()"
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrevise]:        #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38

