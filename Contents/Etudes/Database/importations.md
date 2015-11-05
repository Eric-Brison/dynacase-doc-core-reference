# Importation de documents par CSV {#core-ref:2fb3284a-2424-44b2-93ae-41dc3969e093}
 
Ce chapitre indique comme importer des documents au format
_[CSV][CSV]_ ou _[ODS][ODS]_.



## Attributs multivalués <span class="flag release from">3.3.0</span> {#core-ref:1b8cd020-a2ed-4997-aefe-a4fcbb3564f1}


### MultiValué à un seul niveau de profondeur {#core-ref:17d717f9-6a15-48a9-b5c6-0dc9e52a3993}

Pour les attributs multivalués à un seul niveau (attribut *contenu dans un
    tableau*, ou ayant l'option `multiple=yes` et n'étant pas contenu dans un
    tableau) :

Deux notations sont acceptées. 

La première notation est issue de la notation des [tableaux de
postgreSql][pgarray].

    {"Première valeur","Deuxième valeur","Troisième valeur"}

| index |      valeur      |
| :---: | ---------------- |
|   1   | Première valeur  |
|   2   | Deuxième valeur  |
|   3   | Troisième valeur |


Exemple pour un attribut de type `longtext` contenu dans un tableau, la valeur

    {"Première valeur.\nEt ensuite","Deuxième valeur","Troisième valeur\npour finir."}

correspond à la structure suivante :

| index |               valeur              |
| :---: | --------------------------------- |
|   1   | Première valeur<br />Et ensuite   |
|   2   | Deuxième valeur                   |
|   3   | Troisième valeur<br />pour finir. |

Cette notation permet d'indiquer les retours à la lignes à l'aide des 2 caractères
`\` et `n` (paramètre `csv-linebreak`) ou du caractère de retour chariot`"\n"`.


Il est nécessaire d'échapper les guillemets s'ils sont présents dans le texte.

Le texte suivant :

    {"Première valeur est \"1\","Deuxième valeur est \"2\"","Troisième valeur
    pour finir est \"3\"."}

donne le résultat suivant :

| index |                   valeur                  |
| :---: | ----------------------------------------- |
|   1   | Première valeur est "1"                   |
|   2   | Deuxième valeur est "2"                   |
|   3   | Troisième valeur<br />pour finir est "3". |



La deuxième notation utilise le caractère `\n` comme séparateur de valeur.

**Note** : Cette deuxième notation est conservée pour compatibilité avec la
version précédente. Elle est déclarée obsolète.

    Première valeur\nDeuxième valeur\nTroisième valeur

| index |      valeur      |
| :---: | ---------------- |
|   1   | Première valeur  |
|   2   | Deuxième valeur  |
|   2   | Troisième valeur |
|       |                  |

Cette notation est simple à écrire mais ne permet pas d'indiquer des
retours à la lignes pour les textes longs.



**Note** : la chaîne `<BR>` n'est plus interprétée comme un retour chariot comme
c'est le cas dans la version 3.2.


## MultiValué à deux niveaux de profondeur {#core-ref:c72af782-3573-4916-85b4-f96de0968084}

Pour les attributs multivalués à 2 niveaux (cas des relations ayant l'option
    `multiple=yes` et *contenues dans un tableau*) :

La notation [postgresql][pgarray] permet de définir les valeurs du tableau à 2
dimensions. 

Pour un attribut de type `docid`, ayant l'option `multiple=yes` et contenu
dans un tableau, la valeur 

    {{1236},{6375,8755,564},{567,NULL,4569}}

correspond à la structure suivante :

| index |           relations           |
| :---: | ----------------------------- |
|   1   | • 1236                        |
|   2   | • 6375<br />• 8755<br />• 564 |
|   3   | • 567<br />• <br />• 4569     |

Pour des raisons de compatibilité avec la version précédente la notation
suivante est aussi acceptée.

**Note** : Cette notation est obsolète.

*   la chaîne `\n` délimite deux valeurs de premier niveau,
*   la chaîne `<BR>` délimite deux valeurs de second niveau.

Le texte équivalent à l'exemple ci-dessus est 

    1236\n6375<BR>8755<BR>564\n567<BR><BR>4569




**Note** : Si un délimiteur de texte est défini, le retour chariot est alors
possible sur une ligne et est interprété comme la chaîne `\n`.



<!-- links -->
[CSV]:              http://fr.wikipedia.org/wiki/Comma-separated_values "Comma-separated values sur wikipedia"
[ODS]:              http://fr.wikipedia.org/wiki/OpenDocument "Open Document sur wikipedia"
[hooks]:            #core-ref:8f3d47de-32b5-4748-8a00-b1569c5423e5
[order]:            #core-ref:e41116ee-a682-4033-a7ab-22dc1b99e56a
[doc]:              #core-ref:3acb8fbe-6e5a-4933-95fa-2cea0eae2fc5
[setValue]:         #core-ref:febc397f-e629-4d47-955d-27cab8f4ed2f
[keys]:             #core-ref:7eefc8e7-16a6-4188-99d5-c2c9d817a1fe
[importation]:      #core-ref:a0cb9a84-6bde-476c-b55c-95c8f12abd3a
[preimport]:        #core-ref:adb6ba8b-15c4-42d3-97dc-1da16c2112ae
[postimport]:       #core-ref:9de7e922-150a-416b-b846-b6e195bf0921 
[pgarray]:          http://www.postgresql.org/docs/9.3/static/arrays.html#ARRAYS-INPUT "Tableaux en postgreSql"
