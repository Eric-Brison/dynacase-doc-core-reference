# Utilisateurs, groupes et rôles {#core-ref:2bd98eec-5b03-4af0-b9d6-1bbf78fe9733}
 
## Présentation des comptes {#core-ref:22c7dec6-5ee7-4540-9b3b-7fb4b06d01d9}

Le terme _"compte"_ regroupe les termes _utilisateur_, _groupe_ et _rôle_. 

Les comptes sont composés de :

*   Un objet **_système_**
    
    Il permet les manipulations internes de comptes comme l'affectation de rôle,
    de groupe, etc.
    
    C'est également cet objet qui est utilisé pour tout ce qui concerne le
    [profilage de document][profilage] et les [accessibilités des actions][ACL].
    
    Cet aspect _système_ sera traité dans le chapitre consacré à la classe
    [Account][class_account]<span class="fixme" data-assignedto="nobody">Ajouter le lien vers le chapitre de la classe Account</span>

*   un **_document_**.
    
    Il offre une interface permettant d'effectuer certaines opérations sur
    l'objet système.

Ce chapitre concerne l'aspect _document_ des comptes.

La gestion des utilisateurs peut être faite avec le _centre d'administration_.
L'application _gestion des utilisateurs_ permet de gérer les rôles, groupes et
utilisateurs.

### Vocabulaire {#core-ref:7d0a4094-d975-49fd-8bad-b29c1d46a940}

`Utilisateur`
:   Un document `utilisateur` regroupe les informations permettant à une
    personne de se connecter sur l'interface web de Dynacase. Par extension, un
    `utilisateur` est une personne qui peut se connecter à Dynacase.
    
    La famille décrivant les utilisateurs est **`IUSER`**.

`Groupe`
:   Un document `groupe d'utilisateurs` est une collection qui peut contenir un
    ensemble d'utilisateurs ou de groupe d'utilisateurs.  
    Une arborescence de groupes peut ainsi être constituée à l'aide de ces
    groupes.  
    Un utilisateur ou un groupe d'utilisateurs peut appartenir à plusieurs
    groupes.  
    La seule contrainte est que le graphe des groupes ne doit pas contenir de
    cycle (Le groupe A ne peut pas appartenir au groupe B si B appartient déjà
    au groupe A).
    
    La famille décrivant les groupes d'utilisateurs est **`IGROUP`**.
    
    **Note** : Il existe aussi la famille *"groupe"* (`GROUP`) qui est la
    famille mère de *"groupe d'utilisateur"*. Cette famille de plus haut niveau
    permet de regrouper aussi des documents qui ne sont pas forcément des
    utilisateurs mais des contacts. Dans ce chapitre, le terme `groupe`
    désignera les groupes d'utilisateurs.
    
`Rôle`
:   Un document _"rôle"_ identifie une fonction dans l'organisation. Ce rôle
    sera utilisé pour définir les droits. Un utilisateur peut avoir plusieurs
    rôles.
    
    Contrairement aux groupes, les rôles n'ont pas de hiérarchie.
    
    La famille décrivant les rôles est **`ROLE`**.

<!-- links -->
[profilage]: #core-ref:ce576351-dbe6-45d1-8097-f9573502b651
[ACL]: #core-ref:a98b72ea-c063-4907-abc4-e5171ab55e59
[class_account]: #FIXME