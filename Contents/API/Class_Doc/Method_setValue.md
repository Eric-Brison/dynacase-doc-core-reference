# Doc::setValue() {#core-ref:febc397f-e629-4d47-955d-27cab8f4ed2f}

<div class="short-description">
Modifie la valeur _brute_ d'un attribut de document.
</div>


## Description {#core-ref:5c8d1bc6-d266-4d2d-affa-f754d882f332}

    [php]
    <string> setValue (       string $attributeIdentifier, 
                     string|string[] $value, 
                                 int $index = - 1, 
                                 int &$kvalue = null )

Modifie la valeur d'un attribut de l'objet _Document_. La modification n'est pas
enregistrée en base de données.

### Avertissements {#core-ref:017ec9bc-cb6a-49df-9914-e26cd335518c}

Pour enregistrer la modification , il est nécessaire d'appeler la méthode
[`Doc::store()`][docstore].

Les résultats fournis par la méthode
[`Doc::getAttributeValue()`][docgetattrvalue] ne peuvent pas être utilisés
directement par cette méthode.

## Liste des paramètres {#core-ref:43df765e-53c3-478a-9287-20c78d3bbc8a}

[in] (string) `attributeIdentifier`
:   Identifiant de l'attribut à modifier.

[in] (string|string[]) `value` 
:   Nouvelle valeur **brute**. Dans le cas d'un attribut multiple, il est
    possible d'indiquer les différentes [valeurs brutes][rawvalue] dans un
    tableau.

[in] (int) `index`
:   Dans le cas où l'attribut est multiple, indique l'index de la valeur à 
    modifier.

[out] (array) `kvalue`
:   En cas d'erreur et dans le cas où l'attribut est multiple, indique l'index de 
    la valeur erronée.

## Valeur de retour {#core-ref:371a06e3-7a06-485c-8e44-d5af576e965f}

Message d'erreur. Retourne une chaîne vide s'il n'y a pas d'erreur.

## Erreurs / Exceptions {#core-ref:3b9e376f-b8fa-47b9-8fca-dd1ab55753be}

En cas d'erreur, un message non vide est retourné.
Les principales causes d'erreurs sont :

*   Insuffisance de privilèges. Nécessite le [droit `edit`][profdoc].
*   Attribut inexistant
*   Contenu de la valeur incohérent par rapport au type d'attribut


## Historique {#core-ref:35fed792-7f6b-4e44-8e15-c0db55ac1bab}

Aucun.

## Exemples {#core-ref:4c765c2f-f787-4354-88a5-5102ecb696c6}

Calcul de la somme des attributs `my_numberone` et `my_numbertwo` et
enregistrement dans l'attribut `my_sum`.

Soit la famille suivante :

| BEGIN |                   |     Ma famille    |                  |     | MYFAMILY |         |     |     |     |         |     |
| ----- | ----------------- | ----------------- | ---------------- | --- | -------- | ------- | --- | --- | --- | ------- | --- |
| CLASS | My\MyFamily       |                   |                  |     |          |         |     |     |     |         |     |
| //    | idattr            | idframe           | label            | T   | A        | type    | ord | vis | ... | phpfunc |     |
| ATTR  | MY_IDENTIFICATION |                   | Identification   | N   | N        | frame   | 10  | W   |     |         |     |
| ATTR  | MY_NUMBERONE      | MY_IDENTIFICATION | nombre 1         | Y   | N        | int     | 20  | W   |     |         |     |
| ATTR  | MY_NUMBERTWO      | MY_IDENTIFICATION | nombre 2         | N   | N        | int     | 30  | W   |     |         |     |
| ATTR  | MY_REDACTOR       | MY_IDENTIFICATION | rédacteur        | N   | N        | account | 30  | R   |     |         |     |
| ATTR  | MY_MAIL           | MY_IDENTIFICATION | Adresse courriel | N   | N        | text    | 10  | R   |     |         |     |
| ATTR  | MY_SUM            | MY_IDENTIFICATION | nombre 1&plus;2  | N   | N        | int     | 30  | R   |     |         |     |
| END   |                   |                   |                  |     |          |         |     |     |     |         |     |


### Mise à jour d'attribut après modification du document

Le rédacteur est le dernier à avoir modifié le document.
Calcul de la somme des attributs `my_numberone` et `my_numbertwo` et
enregistrement dans l'attribut `my_sum`.

Avec la classe :

    [php]
    namespace My;
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    
    class MyFamily extends \Dcp\Family\Document
    {
        /**
         * Mise à jour de l'attribut `my_sum` 
         */
        public function setMyRawSum()
        {
            $n1 = intval($this->getRawValue(Aself::my_numberone));
            $n2 = intval($this->getRawValue(Aself::my_numbertwo));
            return $this->setValue(Aself::my_sum, ($n1 + $n2));
        }
        /**
         * Le rédacteur est l'utilisateur courant 
         */
        public function setMyRedactor() {
            return $this->setValue(Aself::my_redactor, getCurrentUser()->fid);
        }
        public function postStore()
        {
            $err = parent::postStore(); 
            if (empty($err)) {
                    $err =$this->setMyRawSum();
                    $err.=$this->setMyRedactor();
            }
            return $err;
        }
    }

## Notes {#core-ref:54e371e6-6336-4020-a5dd-c7174afcbef4}

Aucunes

## Voir aussi {#core-ref:7393c922-cf73-43ae-98b6-4f9148b7161f}

*   [Doc::store()][docstore]
*   [Doc::getOldValue()][docgetoldvalue]
*   [Doc::setAttributeValue()][docsetattrvalue]
*   [Doc::postStore()][docpoststore]

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docgetoldvalue]:   #core-ref:dccf7c64-8f4f-4c4a-8d0d-79b21b924848
[profdoc]:          #core-ref:f1575705-10e8-4bf2-83b3-4c0b5bfb77cf
[rawvalue]:         #core-ref:6302d6cf-bbd1-43ec-a74c-2537581d051c
[docgetattrvalue]:  #core-ref:e4a8d6ff-7229-4105-81c4-94773ac24dfd
[docsetattrvalue]:  #core-ref:1e766800-b2e1-462b-9793-b0261ede8677