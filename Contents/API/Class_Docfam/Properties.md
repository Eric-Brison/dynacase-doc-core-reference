# Propriétés de la classe DocFam {#core-ref:c6e449a1-935c-4f98-b255-d97e8f4d052d}
 

La classe `DocFam` hérite de la classe `Doc`. Elle dispose, par conséquent, des
propriétés de la [classe `Doc`][docprop].

## Particularités sur les propriétés héritées

fromid
:   identifiant de la famille parente.

icon 
:   icone de la famille. Cette icone est aussi utilisée pour les documents
de cette famille.

classname
:   nom de la [classe associée à la famille][famdef].

initid
:   identifiant de la famille. Toujours égal à `id`car les familles ne sont 
    pas révisables.
    
cvid
:   Toujours vide. Non utilisable pour une famille.

dprofid
:   Toujours vide. Une famille ne peut pas avoir de profil dynamique.

revision
:   Toujours 0. Les familles ne sont pas révisables.

state
:   Toujours vide. Les familles ne peuvent avoir de cycle de vie.

wid
:   Identifiant du cycle qui sera lié aux nouveaux documents de cette famille.

title
:   Titre de la famille. Ce titre peut faire l'objet d'une [traduction][i18n].
    Le titre localisé est obtenu avec la méthode `DocFam::getTitle()`.


## Propriétés spécifiques de famille

schar
:   Indique les modalités de révision des documents de cette famille :
    
    *   *R* : Révision automatique à chaque modification,
    *   *S* : document non révisable

cprofid
:   Identifiant du profil qui sera lié aux nouveaux document de la famille.


dfldid 
:   Dossier _racine_ de la famille. Ce dossier est notamment utilisé par
l'application `ONEFAM` via l'action `GENERIC:GENERIC_TAB` qui liste les
documents.
    
    
cfldid
:   Identifiant de recherche ou de dossier par défaut. Cet identifiant est
    utilisé par  l'action `GENERIC:GENERIC_TAB`. Cette recherche est effectuée si
    aucune autre n'est indiquée en paramètre de cette action.

ccvid
:   Identifiant du [contrôle de vue][cvdoc] qui sera lié aux nouveaux documents
    de la famille.

methods
:   Liste des [fichiers _Méthod_][famdef] utilisés pour construire la classe
    de la famille.

maxrev
:   Nombre de révision maximum pour un document de cette famille.
    Si vide ou 0, aucune limite du nombre de révision.
    Si le nombre est positif, une fois le nombre de révision maximum atteint, 
    les révisions les plus anciennes seront supprimées au fur et à mesure des 
    nouvelles révisions. L'historique ne comportera que les `maxrev` dernières
    révisions.

defval
:   Valeurs par défaut pour les nouveaux documents. Ces valeurs sont linéarisés. 
    Elles sont accessibles avec la méthode `DocFam::getDefValues()`.

param
:   Valeurs des paramètres de la famille. Ces valeurs sont linéarisés.
    Elles sont accessibles avec la méthode `DocFam::getParameterRawValue()` ou 
    `Doc::getFamilyParameterValue()`.

 

<!-- links -->
[docprop]:  #core-ref:9aa8edfa-2f2a-11e2-aaec-838a12b40353 "Propriété de la classe Doc"
[famdef]:   #core-ref:17500007-32d8-4aee-bc3f-7e569e1cd5a6 "Déclaration de famille"
[i18n]:     #core-ref:1de9ba03-a3b6-4b56-bfbe-62ce991f8ca1
[cvdoc]:    #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[famintro]: #core-ref:e263d44b-8357-4450-87bf-11cef8bafb24 "Définition d'une famille"