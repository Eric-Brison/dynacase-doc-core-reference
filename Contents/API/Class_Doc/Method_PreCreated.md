# Doc::preCreated() {#core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747}

<div class="short-description" markdown="1">

Hameçon utilisé par la méthode [`Doc::Store()`][docstore]. Elle est appelée
avant l'enregistrement en base de données. Cette méthode doit vérifier si les
conditions de création de document sont valides.

Cette méthode est utilisable aussi pour pré-remplir des attributs avant
l'enregistrement.

Cette méthode est aussi appelé lors de la révision d'un document.

</div>


## Description {#core-ref:4707d4b4-3cad-4d76-8d1d-d9fa75f2fe30}

    [php]
    <string> preCreated ()

Si cette méthode retourne un message d'erreur alors la création sera abandonnée
et la méthode `Doc::store()` retournera le message fournie par cette méthode
afin d'indiquer l'échec.

### Avertissements {#core-ref:014358b2-bf94-4af3-af27-c5de57751a46}

Le document n'a pas encore d'identificateur lors de la création initiale. S'il
s'agit d'une révision, le document possède déjà un identificateur mais celui-ci
sera modifié. L'identificateur initial (`initid`) reste inchangé en cas de
révision.

## Liste des paramètres {#core-ref:347f3a0c-8520-488c-a42f-10c682a2ea32}

Aucun paramètre.

## Valeur de retour {#core-ref:87b533dd-c54b-4235-8608-8d6c6acfc87a}

Message d'erreur. Si la méthode retourne une chaîne de caractère non vide, elle
sera considérée comme un message d'erreur et la création de document sera
abandonnée.

Ce message est aussi stocké dans le paramètre de sortie `$info->error` de la
méthode `Doc::store()`.

## Erreurs / Exceptions {#core-ref:a60d52b1-2de0-4b17-9c30-b149fb8e0af6}

Aucune.

## Historique {#core-ref:19ffa317-5af2-4eed-9c87-d209403a9d8f}

N/A

## Exemples {#core-ref:3a95452a-c163-4c2b-8dc1-01794dc778cf}

Dans la famille _MyFamily_, la création d'un document ne devra être
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
    
    class MyFamily extends \
    Dcp\Family\Document
    {
        public function preCreated()
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



## Notes {#core-ref:3548a3b2-cd44-412e-9ca5-ace8470fc3d1}

N/A

## Voir aussi {#core-ref:e9e47c9a-ab49-4a64-bec8-0db3540456f0}

*   [Doc::store][docstore]
*   [Doc::postCreated][docpostcreated]
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

