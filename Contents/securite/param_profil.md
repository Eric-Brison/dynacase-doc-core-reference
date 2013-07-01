# Paramètres de profilage {#core-ref:fc37efd3-6254-4bc8-8f8d-7f867c852b67}

Les données de paramétrages des règles de paramétrages sont les
[Rôles][roles], les [groupes][groups] et les [utilisateurs][users].
<span class="fixme" data-assignedto="EBR">Je ne comprends pas la phrase</span>

Les profils indiquent un ensemble de règles permettant de déterminer si un
utilisateur à le droit requis pour satisfaire sa requête.

Les vérifications d'accès ne se font que sur les utilisateurs. Les rôles et les
groupes ne pouvant pas se connecter, ils ne servent qu'à propager des droits
vers les utilisateurs.

Les droits peuvent être posés sur les rôles, les groupes et les utilisateurs.

Règles d'affectation :

*   Affectation des rôles :
    1.  Un *utilisateur* peut avoir un ou plusieurs *rôles*.
    1.  Un *groupe* peut être associé à un ou plusieurs *rôles*.
    1.  Un *rôle* ne peut pas avoir de *rôle*.
*   Affectation des groupes :
    1.  Un *utilisateur* peut appartenir à un ou plusieurs *groupes*.
    1.  Un *groupe* peut appartenir à un ou plusieurs *groupes* (arborescence).
    1.  Un *groupe fils* ne peut pas avoir comme enfant un de ses *groupes
        parents* (pas de cycle).
    1.  Un *rôle* ne peut pas appartenir à un *groupe*.

Règles de propagation :

1.  Si un rôle est donné à un utilisateur  
    alors cet utilisateur récupère tous les droits posés sur le rôle.

1.  Si un rôle est associé à un groupe  
    alors tous les membres (utilisateurs) du groupe et de ses sous-groupes
    récupèrent les droits posés sur le rôle.

1.  Les droits posés sur un groupe sont propagés sur tous les membres
    (utilisateurs) du groupe et de ses sous-groupes.

## Exemple {#core-ref:b620d7d0-8eb6-4ffa-89a9-be9a34acf190}

![ Sécurité : Exemple de hiérarchie ](securite/profilaccountgraph.png)

Description de l'exemple ci-dessus :

*   Le rôle _R1_ a les droits _d1_ et _d2_.
*   Le rôle _R2_ a les droits _d3_ et _d2_.
*   Le rôle _R1_ est associé au groupe _G1_.
*   Le groupe _G1_ a les droits _d4_ et _d5_.
*   Le groupe _G2_ appartient au groupe _G1_
*   Le groupe _G2_ a le droit _d8_.
*   L'utilisateur _U1_ a le droit _d6_.
*   L'utilisateur _U1_ appartient au groupe _G2_.
*   L'utilisateur _U2_ n'a pas de droit propre.
*   L'utilisateur _U2_ appartient au groupe _G1_.
*   L'utilisateur _U2_ a le rôle _R2_.


L'exemple ci-dessus, donne les droits suivants :

*   L'utilisateur _U1_ a les droits _d1_, _d2_, _d4_, _d5_, _d6_, _d8_ obtenus
    comme suit :
    *   _d1_, _d2_ récupérés de _R1_,
    *   _d4_, _d5_ récupérés de _G1_,
    *   _d6_ qu'il a en propre,
    *   _d8_ récupéré de _G2_.
*   L'utilisateur _U2_ a les droits _d1_, _d2_, _d3_, _d4_, _d5_ obtenus comme
    suit :
    *   _d1_ récupéré de _R1_,
    *   _d2_ récupéré de _R1_ et _R2_,
    *   _d3_ récupéré de _R2_,
    *   _d4_, _d5_ récupérés de _G1_.


À ces règles, s'ajoute la notion de [suppléant][suppleant]. Le suppléant
récupère les droits du titulaire.

Dans notre cas, si _U2_ est suppléant de _U1_, alors les droits de _U2_ sont :

*   _d1_, _d2_, _d3_, _d4_, _d5_, _d6_, _d8_ obtenus comme suit :
    *   _d1_, _d2_, _d3_, _d4_, _d5_ qu'il a en propre,
    *   _d6_, _d8_ obtenus par suppléance.

## Accès anonyme {#core-ref:2030dc59-1e67-4d3b-84e6-54d468f47bc3}

Si l'accès est fait en mode [anonyme][guest], l'utilisateur utilisé pour
vérifier les droits est *anonymous guest* (login : `anonymous`, nom logique :
`USER_GUEST`). Sur une installation initiale, cet utilisateur n'appartient à
aucun groupe et n'a aucun rôle.




<!-- links -->
[authentification]: #core-ref:b482b82b-ebe2-46e4-8051-c6e83d11a2ae
[actiondef]:        #core-ref:7fcd8c91-b981-4ef6-b4b5-7975a17dbe73 "Définition d'une action"
[suppleant]:        #core-ref:1591eb1c-aead-4f7b-bde9-5f42e397b22e
[users]:            #core-ref:02f32b3d-be94-44f7-9b98-879c6b551c4a
[groups]:           #core-ref:d3a9acde-f4fa-4a0b-8acc-1303f8e6b17e
[roles]:            #core-ref:b9742040-0367-4a3d-a411-7195ec5fa7a4
[guest]:            #core-ref:932e2070-6929-11e2-8218-0021e9fffec1
[document]:         #core-ref:67929e29-abef-437c-88a3-7f43647c60ff "Définition d'un document"
[acls]:             #core-ref:a98b72ea-c063-4907-abc4-e5171ab55e59 "Déclaration de droits applicatifs"
[actionw]:          #core-ref:90bf0711-7874-4c9d-bdf0-7d28becb7628 "Déclaration d'une action"
[wshimport]:        #core-ref:1c97f553-dcba-454e-96a0-8059230065b3 "Importation par wsh"
[CSV]:              http://fr.wikipedia.org/wiki/Comma-separated_values "Comma-separated values sur wikipedia"
[ODS]:              http://fr.wikipedia.org/wiki/OpenDocument "Open Document sur wikipedia"