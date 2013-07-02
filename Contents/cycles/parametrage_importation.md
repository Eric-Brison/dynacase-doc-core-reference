# Paramétrage des cycles de vie {#core-ref:04c63654-156f-4044-8ade-7f5590dfad40}

Les cycles de vie se paramètrent en 4 étapes :

1.  [Importation][importation] de la [famille de Workflow][WF_family]
2.  Création et paramétrage via l'IHM du [document de Workflow][WF_document]
3.  [Exportation][exportation] du [document de Workflow][WF_document]
4.  Association du workflow et de la famille de documents (cf. `WID` dans les
    [propriétés de famille][family_prop])

En effet, lors de l'importation de la famille de workflow, de nombreux attributs
pour chaque état et chaque transition seront crées. Ces attributs vont permettre
de définir le paramétrage avancé pour chacun de ces éléments (couleur de l'état,
envoi de courriel automatique, droits, etc.).

Une fois ces attributs créés, il suffit de les remplir via l'IHM puis d'exporter
le paramétrage ainsi obtenu. Dans l'absolu, il serait possible de générer à la
main le fichier de paramétrage correspondant, mais étant donné le grand nombre
d'attributs générés, cela serait très fastidieux, et donnerait lieu à de
nombreuses erreurs.

<!-- links -->
[importation]: #core-ref:2fb3284a-2424-44b2-93ae-41dc3969e093
[exportation]: #core-ref:8701cd51-0767-4620-8770-57dff9c4460a "Exportation de profil"
[WF_family]: #core-ref:b8824399-f17d-4007-adde-8a7433939273
[WF_document]: #core-ref:a2748e27-7e51-4946-9a80-d23a010e3506
[family_prop]: #core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3