# Exportation des profils  {#core-ref:602c6331-7cdb-4b24-8a56-ffd11e00502f}

L'option d'exportation _"Avec les profils"_ permet d'enregistrer les profils
associés aux documents en plus des données du documents.

Cette option n'est applicable qu'avec le format _"Données réimportables"_.

Si le document a un profil lié alors le document _Profil_ sera aussi exporté.
Si le document a un profil dédié, la clef `PROFIL` portera sur le document même.

Soit les 4 documents suivants :

*   Rotor: Profil lié _ZOO_PRF_CLASSIFICATION_. Ce document possède un nom logique 
    _aliRotor_.
*   Théodor : Profil lié _ZOO_PRF_CLASSIFICATION_. Pas de nom logique.
*   Éléonore : Profil lié _ZOO_PRF_CLASSIFICATION_. Pas de nom logique.
*   Gastor : Profil dédié. Pas de nom logique.

Le fichier _cvs_ produit sera comme décrit ci-dessous :

|   //FAM    |            animal(ZOO_ANIMAL)           |               Identifiant               | Dossier |        nom         |       espèce       |       classe       |             |
| ---------- | --------------------------------------- | --------------------------------------- | ------- | ------------------ | ------------------ | ------------------ | ----------- |
| ORDER      | ZOO_ANIMAL                              |                                         |         | an_nom             | an_espece          | an_classe          |             |
| DOC        | ZOO_ANIMAL                              | aliRotor                                |         | Rotor              | ZOO_ESP_ALLI       | Reptilia           |             |
|            |                                         |                                         |         |                    |                    |                    |             |
| _//FAM_    | _profil de document(PDOC) _             | Identifiant                             | Dossier | titre              | description        | family id          | famille     |
| ORDER      | PDOC                                    |                                         |         | ba_title           | prf_desc           | dpdoc_famid        | dpdoc_fam   |
| DOC        | PDOC                                    | **ZOO_PRF_CLASSIFICATION**              |         | Classification     |                    |                    |             |
| **PROFIL** | **ZOO_PRF_CLASSIFICATION**              |                                         |         | view=ZOO_ROLE_VETO | edit=ZOO_ROLE_VETO | view=ZOO_ROLE_SURV | view=GADMIN |
| **PROFIL** | aliRotor                                | **ZOO_PRF_CLASSIFICATION**              |         |                    |                    |                    |             |
| ORDER      | ZOO_ANIMAL                              |                                         |         | an_nom             | an_espece          | an_classe          |             |
| DOC        | ZOO_ANIMAL                              | TEMPORARY_ZOO_ANIMAL_2079_51a707c53aa48 |         | Théodor            | ZOO_ESP_ALLI       | Reptilia           |             |
| **PROFIL** | TEMPORARY_ZOO_ANIMAL_2079_51a707c53aa48 | ZOO_PRF_CLASSIFICATION                  |         |                    |                    |                    |             |
| DOC        | ZOO_ANIMAL                              | TEMPORARY_ZOO_ANIMAL_2080_51a707c54ae36 |         | Éléonore           | ZOO_ESP_ALLI       | Reptilia           |             |
| DOC        | ZOO_ANIMAL                              | TEMPORARY_ZOO_ANIMAL_3296_51a707c54ce55 | Gastor  | ZOO_ESP_ALLI       | Reptilia           |                    |             |
| **PROFIL** | TEMPORARY_ZOO_ANIMAL_3296_51a707c54ce55 |                                         |         | view=ZOO_ROLE_SURV | view=ZOO_ROLE_VETO | edit=ZOO_ROLE_VETO |             |


Les documents n'ayant pas de nom logique ont un nom logique temporaire. Cet
identifiant  temporaire est supprimé tous les soirs avec le programme _wsh_
"dynacaseDbCleaner". 

La clef `PROFIL` contient l'ensemble des droits explicites mis sur les
[profils][ImportationProfil]. L'affectation des droits est faite avec les noms
logiques des documents _Utilisateurs_,  _Groupes_ et _Rôles_ associés aux
comptes. Si le nom logique n'est pas présent, l'identifiant système du compte
est utilisé.  Attention dans ce cas, il s'agit de l'identifiant du compte et non
du document lié au compte.

Les différents notations de profils sont :

*   [aclName]=[documentName]
*   [aclName]=[accountIdentifier]
*   [attributeName]=[documentName] // Cas des profils dynamiques
*   [attributeName]=[accountIdentifier]


## Exportation de profil de famille

Si le dossier à importer comporte un document _famille_ alors l'exportation du 
profil exportera les documents suivants :

*   Le document profil de la famille 
*   La définition du profil de la famille
*   Le document cycle de vie par défaut de la famille et son profil
*   Les masques du cycles de vie et leur profil
*   Les modèles de mail du cycles de vie et leur profil

|            |                                              |                                           |         |                   |                                      |
| ---------- | -------------------------------------------- | ----------------------------------------- | ------- | ----------------- | ------------------------------------ |
| //FAM      | profil de document(PDOC)                     | Identifiant                               | Dossier | titre             | description                          |
| ORDER      | PDOC                                         |                                           |         | ba_title          | prf_desc                             |
| DOC        | PDOC                                         | ZOO_PRF_CLASSIFICATION                    |         | Classification    |                                      |
| **PROFIL** | ZOO_PRF_CLASSIFICATION                       |                                           |         | view=GADMIN       | viewacl=GADMIN                       |
| //FAM      | modèle de mail(MAILTEMPLATE)                 | Identifiant                               | Dossier | Titre             | Famille                              |
| ORDER      | MAILTEMPLATE                                 |                                           |         | tmail_title       | tmail_family                         |
| DOC        | MAILTEMPLATE                                 | TEMPORARY_MAILTEMPLATE_3801_51a8c23b99679 |         | Couriel rédacteur | ZOO_DEMANDEADOPTION                  |
| //FAM      | profil de document(PDOC)                     | Identifiant                               | Dossier | titre             | description                          |
| ORDER      | PDOC                                         |                                           |         | ba_title          | prf_desc                             |
| DOC        | PDOC                                         | PRF_ADMIN_EDIT                            |         | Administration    | lecture seule sauf pour groupe admin |
| **PROFIL** | PRF_ADMIN_EDIT                               |                                           |         | view=GDEFAULT     | edit=GADMIN                          |
| **PROFIL** | TEMPORARY_MAILTEMPLATE_3801_51a8c23b99679    | PRF_ADMIN_EDIT                            |         |                   |                                      |
| //FAM      | Cycle demande Adoption(ZOO_WDEMANDEADOPTION) | Identifiant                               | Dossier | titre             | description                          |
| ORDER      | ZOO_WDEMANDEADOPTION                         |                                           |         | ba_title          | wf_desc                              |
| DOC        | ZOO_WDEMANDEADOPTION                         | ZOO_CYCLEDA                               |         | Défaut            |                                      |
| //FAM      | profil de document(PDOC)                     | Identifiant                               | Dossier | titre             | description                          |
| ORDER      | PDOC                                         |                                           |         | ba_title          | prf_desc                             |
| DOC        | PDOC                                         | ZOO_PRF_HYGIENE                           |         | Hygiène           |                                      |
| **PROFIL** | ZOO_PRF_HYGIENE                              |                                           |         | view=GADMIN       | viewacl=GADMIN                       |
| //FAM      | masque de saisie(MASK)                       | Identifiant                               | Dossier | titre             | Famille                              |
| ORDER      | MASK                                         |                                           |         | ba_title          | msk_famid                            |
| DOC        | MASK                                         | TEMPORARY_MASK_3802_51a8c23bac7c6         |         | Initialisé        | ZOO_DEMANDEADOPTION                  |
| **PROFIL** | TEMPORARY_MASK_3802_51a8c23bac7c6            | PRF_ADMIN_EDIT                            |         |                   |                                      |
| //FAM      | profil de famille(PFAM)                      | Identifiant                               | Dossier | titre             | description                          |
| ORDER      | PFAM                                         |                                           |         | ba_title          | prf_desc                             |
| DOC        | PFAM                                         | ZOO_PRF_FAM                               |         | Profil Zoo        | Pour les familles du zoo             |
| **PROFIL** | ZOO_PRF_FAM                                  |                                           |         | edit=GADMIN       | viewacl=GADMIN                       |
|            |                                              |                                           |         |                   |                                      |
| BEGIN      |                                              |                                           |         |                   | ZOO_DEMANDEADOPTION                  |
| **PROFID** | ZOO_PRF_FAM                                  |                                           |         |                   |                                      |
| WID        | ZOO_CYCLEDA                                  |                                           |         |                   |                                      |
| END        |                                              |                                           |         |                   |                                      |

Les masques et les modèles de mail auront un nom logique temporaire s'ils n'ont
pas de nom logique.   
Le fichier exporté comporte aussi, à la fin, le paramétrage
du profil et du cycle  pour la famille exporté.

**Note** : Les documents "_"famille"_ (caractéristiques et structures) ne sont
 pas exportables. Seul leur profil est exportable avec cette option.

<!-- links -->
[ImportationProfil]: #core-ref:ce576351-dbe6-45d1-8097-f9573502b651