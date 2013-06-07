# Le document de workflow {#core-ref:b541e22f-5ece-4d19-8460-0cb0c5f3ec7a}

Une fois la classe de workflow correctement importée, il est possible de créer
un document de cette famille.

Le document ainsi créé permet de paramétrer finement le comportement des
documents liés à ce workflow.

Il est possible de paramétrer :

*   le titre du workflow
*   une description
*   la famille à laquelle ce workflow peut être attaché
*   la famille à utiliser pour le [profilage dynamique][dynprof]
*   pour chaque état
    *   le profil à appliquer aux documents à cet état
    *   le masque à appliquer aux document à cet état
    *   la couleur de cet état
    *   le contrôle de vue à appliquer aux documents à cet état
    *   les mails à envoyer lorsqu'un document arrive dans cet état
    *   les minuteurs à attacher à un document lorsqu'il arrive dans cet état
*   pour chaque transition
    *   les mails à envoyer lorsque cette transition est effectuée
    *   les minuteurs à attacher à un document lorsqu'il suit cette transition
    *   les minuteurs persistants à attacher à un document lorsqu'il suit cette
        transition
    *   les minuteurs persistants à détacher d'un document lorsqu'il suit cette
        transition

## Titre {#core-ref:f7f12788-314b-4949-b4bc-bc3dc8d68269}

Le titre est utilisé dans l'historique des documents suivant ce workflow.

## Description {#core-ref:6c3a7d11-70d8-4402-b21d-6689c125e58e}

La description n'est pas utilisée en dehors du document de workflow.

## la famille {#core-ref:a959a5d9-1349-4dbe-8eea-8a2ef70d0162}

La famille permet de restreindre les documents auquel ce workflow peut être
attaché : seuls les document de cette famille et de ses sous familles peuvent
dépendre de ce workflow.

## Paramétrage par état {#core-ref:fe460151-599e-4a45-b566-4d8a3041461c}

### Profil {#core-ref:90dea5a4-e99e-496f-8542-3af0486e150a}

Lorsqu'un document arrive dans cet état, le profil identifié par cette relation
lui est attaché.

**Attention**, cet attachement ne se fait que lors du changement d'état. Aussi,
si la valeur de cet attribut est changée, les documents qui sont déjà dans cet
état garderont leur profil.

### Masque {#core-ref:8e654bad-2f93-4c9b-9961-5bc7b6ab6cb3}

Lorsqu'un document est dans cet état, sa consultation et sa modification sont
soumises au [masque][MASK] identifié par cette relation.

**Attention**, cette valeur est récupérée à chaque accès au document. Aussi, si
la valeur de cet attribut est changée, les documents à cet état sont directement
impactés.

### Couleur {#core-ref:2d443d10-041c-4cfb-a261-28e04dbd28ba}

Lorsqu'un document est dans cet état, cette couleur lui est associée. Elle est
utilisée par les interfaces standard de Dynacase.

Cette couleur doit être au format hexadécimal (#RRGGBB).

**Attention**, cette valeur est récupérée à chaque accès au document. Aussi, si
la valeur de cet attribut est changée, les documents à cet état sont directement
impactés.

### Contrôle de vue {#core-ref:a51d9c50-d17b-4b69-bd3b-fad94db6da65}

Lorsqu'un document arrive dans cet état, le [contrôle de vue][CVDOC] identifié
par cette relation lui est attaché.

**Attention**, cet attachement ne se fait que lors du changement d'état. Aussi,
si la valeur de cet attribut est changée, les documents qui sont déjà dans cet
état garderont leur contrôle de vue.

**Attention**, si un état définit un masque et un contrôle de vue, seul le
contrôle de vue sera pris en compte, et le masque sera ignoré.

### Modèle de courriel {#core-ref:b270ff85-90f1-4fcf-ae6e-e826b65c3eff}

Lorsqu'un document arrive dans cet état, les [Modèle de mail][MAILTEMPLATE]
identifiés par cette relation sont envoyés à partir du document.

En plus des clés spécifiques au document, le workflow ajoute :

*   les [Paramètres de transition][transition_parameter]
*   le commentaire fourni à la [confirmation][transition_confirmation] (dans la
    clé `WCOMMENT`)

#### Minuteur {#core-ref:a2748e27-7e51-4946-9a80-d23a010e3506}

Lorsqu'un document arrive dans cet état, les [minuteurs][TIMER] identifiés par
cette relation sont attachés au document.

Si le document possède déjà des minuteurs, les nouveaux seront ajoutés.

**Attention**, cet attachement ne se fait que lors du changement d'état. Aussi,
si la valeur de cet attribut est changée, les documents qui sont déjà dans cet
état garderont leurs minuteurs.

**Attention** Si le document possède déjà une instance du minuteur à attacher,
alors l'instance existante est réinitialisée <span class="fixme"
data-assignedto="EBR">C'est vrai?</span>

Lorsque le minuteur quitte cet état, les minuteurs étant définis à cet état sont
détachés du document.

**Attention** Lorsque le document quitte cet état, les instances de tous les
minuteurs correspondant à cet état sont détachées, qu'ils aient été attachés par
cet état, ou par tout autre moyen.

## Paramétrage par activité {#core-ref:703f4350-64df-4b1c-a25f-0d040b34f36b}

### Modèle de courriel {#core-ref:43a1b1bf-3807-48e0-954d-a6bb3345bfa4}

Lorsqu'un document suit cette transition, les [Modèle de mail][MAILTEMPLATE]
identifiés par cette relation sont envoyés à partir du document.

En plus des clés spécifiques au document, le workflow ajoute :

*   les [Paramètres de transition][transition_parameter]
*   le commentaire fourni à la [confirmation][transition_confirmation] (dans la
    clé `WCOMMENT`)

### Minuteur {#core-ref:0c1a2bdc-ee8c-46f1-a463-cb0094b34364}

Lorsqu'un document suit cette transition, les [minuteurs][TIMER] identifiés par
cette relation sont attachés au document.

Si le document possède déjà des minuteurs, les nouveaux seront ajoutés.

**Attention**, cet attachement ne se fait que lors du changement d'état. Aussi,
si la valeur de cet attribut est changée, les documents qui sont déjà dans cet
état garderont leurs minuteurs.

**Attention** Si le document possède déjà une instance du minuteur à attacher,
alors l'instance existante est réinitialisée <span class="fixme"
data-assignedto="EBR">C'est vrai?</span>

<span class="fixme" data-assignedto="EBR">ils sont détachés quand?</span>

### Minuteurs persistant à attacher {#core-ref:1844ba53-3e58-4588-8e9d-63a92d2f62a8}

Lorsqu'un document suit cette transition, les [minuteurs][TIMER] identifiés par
cette relation sont attachés au document.

Si le document possède déjà des minuteurs, les nouveaux seront ajoutés.

**Attention**, cet attachement ne se fait que lors du changement d'état. Aussi,
si la valeur de cet attribut est changée, les documents qui sont déjà dans cet
état garderont leurs minuteurs.

**Attention** Si le document possède déjà une instance du minuteur à attacher,
alors l'instance existante est réinitialisée <span class="fixme"
data-assignedto="EBR">C'est vrai?</span>

Ces minuteurs ne seront jamais détachés automatiquement, et doivent être
détachés au moyen de l'attribut Minuteurs persistant à détacher.

### Minuteurs persistant à détacher {#core-ref:da352279-c1a4-41c9-a5d3-2aeeabc61f74}

Lorsqu'un document suit cette transition, les [minuteurs][TIMER] identifiés par
cette relation sont détachés du document.

**Attention** Lorsque le document suit cette transition, les instances de tous
les minuteurs correspondant à cet attribut sont détachées, qu'ils aient été
attachés par cet état, ou par tout autre moyen.

<!-- links -->
[dynprof]: #core-ref:bc24834a-b380-4681-ae94-08b93076a7e8
[MASK]: #core-ref:327ad491-06df-4e5b-b49a-695c75439fe1
[CVDOC]: #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[MAILTEMPLATE]: #core-ref:8723b1aa-10d3-4316-af6b-071f4d59ceee
[TIMER]: #core-ref:3de1c186-e1ab-44a3-b3b1-536d2f9a7554
[transition_parameter]: #core-ref:a808e6bc-67f8-4666-b5ec-e9bc429a0eb5
[transition_confirmation]: #core-ref:a808e6bc-67f8-4666-b5ec-e9bc429a0eb5