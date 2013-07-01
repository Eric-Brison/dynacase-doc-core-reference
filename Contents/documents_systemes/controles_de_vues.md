# Contrôle de vue {#core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0}
 
Les contrôles de vue permettent de spécifier des représentations alternatives
pour un document. L'utilisateur pourra choisir parmi ces représentations, en
fonction de ses droits, ou alors le contrôle de vue pourra déterminer dynamique
la vue en fonction de l'utilisateur, et toujours de ses droits.

Chaque modalité de représentation est appelée une *vue*.

Chaque vue est composées de :

**un identifiant système** (obligatoire)
:   une chaîne alphanumérique, qui doit être unique au sein du contrôle de vue.
    Elle permet de désigner la vue de manière non ambiguë.

**un libellé** (obligatoire)
:   une chaîne permettant de désigner la vue à l'utilisateur. Traduisible, elle
    sera notamment utilisée dans les menus.

**un type** (obligatoire)
:   *consultation* ou *édition*, détermine pour quelle type de représentation
    la-dite vue est utilisable.

une *zone* (sous la forme `APP:ZONE:OPTIONS:TRANSFORMATION`)
:   permet d'indiquer un template de représentation. se reporter à 
    [vues de documents][document_view] pour
    plus de précisions.

un *masque*
:   permet de spécifier un [masque][masque] à appliquer lors de l'utilisation de
    cette vue

un numéro d'*ordre*
:   entier strictement positif (**Attention** : une vue avec l'ordre 0 n'est pas
    prise en compte, il permet d'indiquer un ordre de préférence pour les vues.

un caractère *affichable*
:   indique si la vue doit être présentée à l'utilisateur sous forme de menu
    (pour lui permettre de choisir cette représentation), ou ne sera accessible
    que par programmation.
    
    Si la vue est affichable, alors elle sera présentée au moyen de son libellé.

un nom de *menu*
:   si la vue est affichable, indique le libellé du menu sous lequel doit être
    présentée la vue
    
## Profilage du contrôle de vue {#core-ref:742f93b5-9df6-4cad-be22-1fd8eb6a76ef}

Il est possible d'appliquer un [profil][cvprofil] à un contrôle de vue. Ce profile détermine
alors pour chaque vue qui a le droit d'y accéder.

Le profil en question peut être statique, mais également dynamique.

## Choix automatique de la vue {#core-ref:b74b3617-2085-47f8-9172-9f35c0290b5a}

La vue à utiliser peut être explicitement spécifiée au moyen du paramètre d'url
`vid=[VIEW_ID]` où `[VIEW_ID]` est l'*identifiant système* de la vue à
utiliser. Dynacase va alors vérifier que l'utilisateur a bien accès à la vue
spécifiée. Dans le cas contraire, un message d'erreur est retourné. Si le
paramètre `vid` référence une vue non existante, ou lorsqu'aucune vue n'est
spécifiée, la vue est automatiquement choisie selon le mécanisme suivant :

1.  restriction à la liste des vues pour lesquelles
    *   le *type* correspond à l'action courante,
    *   l'utilisateur [est autorisé à y accéder][cvprofil],
2.  classement des vues restantes par numéro d'*ordre* croissant
,
3.  utilisation de la première des vues restantes.
    Si aucune des vues n'est utilisable, c'est la vue par défaut qui est
    utilisée.


## libellé du menu *modifier* {#core-ref:bcf1d848-9abb-4260-a4c1-0c6fd5abc3c9}

Lors de la consultation, le libellé du menu *modifier* correspondra au libellé
de la vue de modification choisie selon l'algorithme précédent.

## Astuces {#core-ref:2c014979-7901-48be-ab15-89e107f0065b}

Les ordres ne sont pas obligés de se suivre. Aussi, vous pouvez numéroter vos
vues de 10 en 10, afin de faciliter l'ajout futur d'une nouvelle vue.

Il est recommandé de restreindre la visibilité des attributs sur la famille,
et d'élargir ces visibilités au moyen des contrôles de vue et des masques
associés. Ainsi, il devient aisé d'avoir une vue d'administration, utilisant un
masque dédié, et ayant le plus faible ordre, et les autres vues restreintes,
sans masque et avec un ordre supérieur.

<!-- links -->
[masque]: #core-ref:327ad491-06df-4e5b-b49a-695c75439fe1 "Définition d'un masque"
[document_view]: #core-ref:cb3e2b97-ee6d-4cdf-aa25-b2e41d0d3156
[cvprofil]: #core-ref:65603797-5d8a-4a0d-954a-2dc69b5af11e "Détail sur le profilage d'un contrôle de vue"