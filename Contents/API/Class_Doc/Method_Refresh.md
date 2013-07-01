# Doc::Refresh() {#core-ref:0bab02de-50e0-46f2-8bdb-81c62dc86c93}

<div class="short-description">
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

Cette méthode est appelé 

### Avertissements {#core-ref:9ac95508-ad63-4b73-a757-5e7743a97b3c}

<span class="fixme template">Avertissements</span>

## Liste des paramètres {#core-ref:c80fba75-e3c2-4da6-9ecd-fa5c55b88bc8}

<span class="fixme template">Liste des paramètres</span>

<div class="fixme template">
exemple:  
[out] (array) `info`
:   Si `info`est fourni, il sera rempli avec les informations de l'image (taille, couleur, etc.).
</div>

## Valeur de retour {#core-ref:b8232c52-0bcb-45f6-87ea-4d5b1be1e28d}

Cette méthode retourne les message fournis par les hameçons `preRefresh() et
`postRefresh()`. Ce message est présenté sur l'interface web de consultation de
document lors de l'affichage du document.


## Erreurs / Exceptions {#core-ref:83715503-3396-423a-b16e-01f49d3cb045}

<span class="fixme template">Erreurs / Exceptions</span>

## Historique {#core-ref:70daceb9-e49d-403f-994a-a56c3e8baa50}

<span class="fixme template">Historique</span>

## Exemples {#core-ref:5689d00a-e345-48ec-b7eb-76f18d30c0d9}

<span class="fixme template">Exemples</span>

## Notes {#core-ref:9faf3176-7874-4bb9-97e8-b2004f88b7f6}

<span class="fixme template">Notes</span>

## Voir aussi {#core-ref:73156d50-77d9-4c1a-a5fc-ba9defb9ad5c}

*   [Doc::preRefresh][docprerefresh]
*   [Doc::postRefresh][docpostrefresh]

<!-- links -->
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrefresh]:       #core-ref:0bab02de-50e0-46f2-8bdb-81c62dc86c93
[computeattr]:      #core-ref:4565cab9-73c8-4eee-bfa7-218ffbd4b687 "Attributs calculés"