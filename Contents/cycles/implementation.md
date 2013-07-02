# Aperçu de l'implémentation {#core-ref:91e2017b-d595-47b3-bfc6-3b57c932b989}

Un cycle de vie est structuré au moyen d'une *famille de workflow* et d'un
*document de workflow*.

La *famille de workflow* permet de spécifier :

*   le graphe du cycle :
    *   la liste des étapes,
    *   la liste des méthodes déclenchées par chaque transition,
*   les attributs spécifiques au cycle. Ces attributs peuvent être utilisés dans 
    les traitements des transitions et sont différents pour chaque instance de 
    cycle de vie.
*   les paramètres de familles qui seront utilisables lors des traitements
    spécifiques liés aux cycles : pour chaque étape et chaque transition, un
    ensemble de paramètres est généré à partir de la structure.

Le *document de workflow* permet de spécifier le paramétrage :

*   des minuteurs, mails, etc. déclenchés à chaque étape ou transition
*   des acteurs et de [leurs droits][wprofil] au fil des différentes étapes 
    du cycle

Généralement une *famille de workflow* ne produit qu'un seul *document
workflow*. Ce *document workflow* est ensuite utilisé pour gérer la vie de tous
les documents d'une famille. Il est toutefois possible de créer plusieurs
*documents workflow* issus d'une même famille avec des paramétrages différents.
Ils auront en commun la définition du cycle mais pourront avoir des paramétrages
différents.   Ainsi, par exemple :

*   sur une étape E1,
    *   un courriel au directeur sera envoyé pour le cycle C1
    *   un courriel au contrôleur sera pour le cycle C2.

De plus chacun des *documents workflow* possède sa propre définition de droits.
Ainsi, ce ne sont pas les mêmes acteurs qui jouent les différents rôles de
contrôleur, ou de rédacteur.

## Les transitions {#core-ref:ed74f035-ec6f-4e63-ae61-014a2947a6aa}

Un type de transition est composé  :

*   de deux conditions de passage de transition : `m0` et `m1`,
*   de deux traitements : `m2` et `m3`,
*   d'une confirmation du passage de la transition : `nr`,
*   d'une demande de paramètres de transition : `ask`.

Une transition suit le déroulement suivant :


![Processus de transition ](cycle/Sequence_transition.png)



La méthode `m0` est aussi utilisée lors de l'affichage des menus de transitions
afin de n'afficher que les transitions autorisées. Les messages d'erreur des
méthodes `m0` sont affichés sur le menu (lors du survol) afin d'indiquer la
raison de l'erreur.


![Processus d'affichage du menu des transitions](cycle/Sequence_transition_menu.png)

<span class="fixme" data-assignedto="MCO">Détail de m0->m3 dans famille de workflow. 
  Mettre en suivant que l'aspect théorique ( si possible)</span>



### `m0` {#core-ref:c3bcdf20-5756-4880-b067-36f0d62b68c5}

`m0` fait référence à une méthode de la classe de workflow. Cette méthode sert
à déterminer si le document est tel qu'il permet d'envisager la transition.

C'est la toute première méthode appelée lors d'une demande de transition.

Elle reçoit en paramètres :

1.  l'identifiant de la prochaine étape, (étape d'arrivée)
2.  l'identifiant de l'étape actuelle, (étape de départ)
3.  le message de confirmation (si la méthode est exécuté pour l'affichage 
    des menus, le message est vide)

<span class="fixme" data-assignedto="MCO">Indiquer plus explicitement la signature</span>

Si elle retourne une chaîne vide, alors la transition peut être effectuée. dans
le cas contraire, elle doit retourner un message localisé qui indiquera à
l'utilisateur la raison pour laquelle la transition ne peut pas être effectuée.

*Note* : Cette méthode est aussi appelée lors de l'affichage de la liste des
états accessibles. Cela permet notamment de signaler à l'utilisateur les
transitions qu'il a le droit d'effectuer, mais pour lesquelles il doit faire des
modifications sur le document. De fait, cette méthode ne **doit pas modifier le
document**.

### Paramètres de transition {#core-ref:9e248e52-ad6b-4089-ab83-11a534b307e9}

Les *paramètres de transition* sont des [paramètres][family_parameters] du cycle
de vie, qui sont demandés à l'utilisateur lors de la transition. Ils doivent
être définis sur la famille de cycle de vie, et référencés dans la transition au
moyen de la clé `ask`. Cette clé contient un tableau des identifiants de tous
les paramètres à utiliser.

Comme dans un document, l'interface correspondant à ces paramètres sera générée
par Dynacase ; les paramètres sont demandés par l'intermédiaire d'une fenêtre
modale.

**Attention** :Contrairement aux [paramètres de famille
ordinaires][family_parameters], les contraintes ne sont pas prises en compte
dans les paramètres de transition.

### Confirmation {#core-ref:a808e6bc-67f8-4666-b5ec-e9bc429a0eb5}

si `nr` n'est pas positionné à `true`, alors une confirmation est demandée.
Cette confirmation demande la raison de la transition. Cette raison est facultative. 

Cette raison est affichée dans le même fenêtre que les paramètres de
transition. Elle est enregistré dans l'historique du document.

### `m1` {#core-ref:603b0905-6269-4dca-a656-55e1d5524c3a}

`m1` fait référence à une méthode de la classe de workflow. Cette méthode
sert à modifier le document juste avant le changement d'état.
C'est le document tel qu'il est à l'issue de la méthode `m1` qui sera sauvegardé
dans l'historique du document.

Elle reçoit en paramètres :

1.  l'identifiant de la prochaine étape, (étape d'arrivée)
2.  l'identifiant de l'étape actuelle, (étape de départ)
3.  le message de confirmation

<span class="fixme" data-assignedto="MCO">Indiquer plus explicitement la signature</span>

Si elle retourne une chaîne vide, alors la transition peut être effectuée. dans
le cas contraire, elle doit retourner un message localisé qui indiquera à
l'utilisateur la raison pour laquelle la transition ne peut pas être effectuée.


<span class="fixme" data-assignedto="MCO">Indiquer comment on récupère les ask</span>

### `m2` {#core-ref:ced2bc66-792e-4c55-bd0a-dcca09e9732d}

`m2` fait référence à une méthode de la classe de workflow. Cette méthode sert à
modifier le document juste après le changement d'état. C'est le document tel
qu'il est à la suite de `m2` qui sera soumis aux minuteurs et envoyé par mail.

1.  l'identifiant de l'étape actuelle, (étape de départ)
2.  l'identifiant de la prochaine étape, (étape d'arrivée)
3.  le message de confirmation

<span class="fixme" data-assignedto="MCO">Indiquer plus explicitement la signature</span>
Puisque `m2` intervient après le changement d'état, cette méthode n'est pas
bloquante. Aussi, retourner une chaîne d'erreur n'interrompt pas le processus
(mais le message d'erreur sera bien affiché à l'utilisateur à l'issue de la
transition).
<span class="fixme" data-assignedto="MCO">Indiquer comment on récupère les ask</span>

### `m3` {#core-ref:39462cd9-7962-4efe-888b-912d7256671a}

`m3` fait référence à une méthode de la classe de workflow. Cette méthode est la
dernière exécutée au cours de la transition (c'est à dire qu'elle intervient
après les différents traitements automatiques effectués par Dynacase).

1.  l'identifiant de l'étape actuelle, (étape d'arrivée)
2.  l'identifiant de l'ancienne étape, (étape de départ)
3.  le message de confirmation

<span class="fixme" data-assignedto="MCO">Indiquer plus explicitement la signature</span>
Elle n'est utile que dans de très rares cas, et est en particulier utilisée
lorsqu'une seconde transition doit être déclenchée automatiquement à l'issue de
la première.
<span class="fixme" data-assignedto="MCO">Indiquer comment on récupère les ask</span>

## Le graphe {#core-ref:d176f897-3dae-46b5-834c-9b20dcd41c7d}

Le graphe est constitué d'un ensemble de triplets

*   État de départ
*   État d'arrivée
*   Une transition

Une fois assemblés, ces triplets définissent un Cycle de vie.

<!-- links -->
[family_parameters]: #core-ref:4595c8e7-5002-4dbc-b6bb-882b4123efd8
[wprofil]:           #core-ref:226eb791-83f5-4f6a-9ea1-bddc74cf9e73