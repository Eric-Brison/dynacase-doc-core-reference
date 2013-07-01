# Doc::postStore() {#core-ref:99520a31-0aef-4bc6-b20a-114737059d17}

<div class="short-description" markdown="1">
Hameçon utilisé par la méthode [`Doc::Store()`][docstore]`. Cette méthode est
appelé après l'enregistrement en base de données
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description {#core-ref:6a794ff2-4c9c-4bb1-aed7-8c23e3b7ab2d}

    [php]
    <string> postStore ()

Cette méthode est utilisable aussi pour réaliser un post-traitement après une
modification. Elle ne peut pas annuler l'enregistrement. Le document possède un
identificateur est déjà enregistré en base.

### Avertissements {#core-ref:a3f912a9-0ccf-4f38-97af-faeac7c423aa}

Il ne faut pas appeler la méthode Doc::store() dans cette méthode au risque
d'avoir une boucle infinie.

Si des modifications d'attributs sont réalisées dans cette méthode, ils seront
enregistrés en base par la méthode `Doc::store()`.


## Liste des paramètres {#core-ref:0252e614-71e3-44f8-a4d8-6bc5ea238ce2}

Aucun paramètre.

## Valeur de retour {#core-ref:5ceded6d-ae21-4c1e-b554-537b532aed23}

La valeur de retour est un message d'information. Il sera stocké dans le
paramètre de sortie `$info->postStore` de la méthode `Doc::store()`.

## Erreurs / Exceptions {#core-ref:e187697c-5e99-4083-ab9d-05d2a6056435}

N/A

## Historique {#core-ref:265bde3d-c9a9-4976-8a57-e9c4c980b73c}

Anciennement nommé `postModify()`.

## Exemples {#core-ref:47b6948d-d6a5-4b04-b96d-8657499dc5c2}

<span class="fixme template">Exemples</span>

## Notes {#core-ref:339dfc65-e878-4451-9145-f7e70b729cf5}

N/A

## Voir aussi {#core-ref:ade45758-e063-4c80-8694-6a49f0845270}

*   [Doc::store][docstore]
*   [Doc::preCreated][docprecreated]
*   [Doc::preStore][docprestore]
*   [Doc::postCreated][docpostcreated]

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpostcreated]:   #core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45 "Hameçon Doc::postCreated()"
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docprestore]:      #core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0 "Hameçon Doc::preStore()"
[docprecreated]:    #core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747 "Hameçon Doc::preCreated()"
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrevise]:        #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38

