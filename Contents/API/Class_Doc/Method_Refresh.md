# Doc::refresh() {#core-ref:0bab02de-50e0-46f2-8bdb-81c62dc86c93}

<div class="short-description" markdown="1">
Méthode utilisé pour mettre à jour les [attributs calculés][computeattr].
</div>
<!--
<div class="applicability">
Obsolète depuis #.#.#
</div>
-->

## Description {#core-ref:e8acacec-8062-4c49-944e-57e2e79c83d4}

    [php]
    <string> refresh ()

Cette méthode est appelée depuis l'interface lors de la consultation du document
unitaire mais pas depuis les interfaces présentant les listes de documents.

Cette méthode est appelée depuis la méthode [`Doc::store()`][docstore].

### Avertissements {#core-ref:9ac95508-ad63-4b73-a757-5e7743a97b3c}

Aucun.

## Liste des paramètres {#core-ref:c80fba75-e3c2-4da6-9ecd-fa5c55b88bc8}

Aucun paramètre.

## Valeur de retour {#core-ref:b8232c52-0bcb-45f6-87ea-4d5b1be1e28d}

Cette méthode retourne les message fournis par les hameçons
[`preRefresh()`][docprerefresh] et [`postRefresh()`][docpostrefresh]. Ce message
est présenté sur l'interface web de consultation de document lors de l'affichage
du document.


## Erreurs / Exceptions {#core-ref:83715503-3396-423a-b16e-01f49d3cb045}

Aucune.

## Historique {#core-ref:70daceb9-e49d-403f-994a-a56c3e8baa50}

Aucun.

## Exemples {#core-ref:5689d00a-e345-48ec-b7eb-76f18d30c0d9}

Actualisation d'un ensemble de documents.

    [php]
    $s=new SearchDoc("", "MYFAMILY");
    $s->setObjectReturn();
    $dl=$s->search()->getDocumentList();
    
    $messages=array();
    /** @var Doc $doc */
    foreach ($dl as $doc) {
        $messages[$doc->id]=$doc->refresh();
    }

## Notes {#core-ref:9faf3176-7874-4bb9-97e8-b2004f88b7f6}

Lors de l'actualisation du document les hameçons suivants sont lancés :

1.  [`Doc::preRefresh()`][docprerefresh]  
    Calcul des attributs calculés.
1.  [`Doc::postRefresh()`][docpostrefresh]  
    Enregistrement en base si modification détectée

Les affectations des [attributs calculés][computeattr] sont réalisées par la
méthode `specRefreshGen()` qui est générée lors de l'importation de la famille.
Cette méthode est appelée entre les hameçons
[`Doc::preRefresh()`][docprerefresh] et  [`Doc::postRefresh()`][docpostrefresh].

## Voir aussi {#core-ref:73156d50-77d9-4c1a-a5fc-ba9defb9ad5c}

*   [Doc::preRefresh][docprerefresh]
*   [Doc::postRefresh][docpostrefresh]

<!-- links -->
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrefresh]:       #core-ref:0bab02de-50e0-46f2-8bdb-81c62dc86c93
[computeattr]:      #core-ref:4565cab9-73c8-4eee-bfa7-218ffbd4b687 "Attributs calculés"
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12