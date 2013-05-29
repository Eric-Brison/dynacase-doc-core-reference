# Vue OpenDocument Text {#core-ref:d03e0905-2be1-4649-a823-9f64e94cba29}

Une vue openDocument text permet de générer une *représentation bureautique* du
document. Cette représentation est au format *odt*, et peut être convertie en
*pdf*, ou autre format bureautique, au moyen du [moteur de transformation][TE].

Étant donné que cette représentation est binaire, il y a de nombreuses
différences entre les vues OpenDocument Text et les représentations html.

Il est à noter que les vues openDocument text ne sont utilisables que pour la
consultation.

Une vue OpenDocument Text est composée de :

*   un fichier de template (au format *odt*), définissant la structure,
*   une méthode (appelée *contrôleur de vue*) du document à représenter,
    définissant les valeurs.  
    Cette méthode peut également être omise. Dans ce cas, dynacase fera appel
    au [contrôleur de vue par défaut][default_view_controleur].

<span class="fixme" data-assignedto="EBR">préciser les règles de casse</span>

## Le contrôleur de vue {#core-ref:a7e88a30-c481-4e94-975f-c91c2eb4257d}

Pour qu'une méthode du document soit utilisable en tant que contrôleur d'une
vue, il est nécessaire de lui ajouter la phpDoc `@templateController` afin
de se prémunir d'une éventuelle exécution arbitraire de code.

Les paramètres reçus par la méthode sont au nombre de 3 :

*   `$target` (string): `"ooo"` ;
*   `$ulink` (booléen) : `false` ;
*   `$abstract` (booléen) : indique s'il faut générer uniquement les
    attributs de la fiche résumé (`false` par défaut).

Par convention :

*   le fichier de template porte l'extension odt,
*   son nom (en minuscule) détermine le nom de la vue,
*   la méthode associée doit porter le même nom (la casse du nom de la méthode
    n'est pas prise en compte).  
    L'objet `Layout` est accessible au moyen de la propriété `lay` de l'objet
    courant (`$this->lay`).

### Contrôleur par défaut {#core-ref:303fbb4d-a688-4fd7-8329-bbc799251889}

En l'absence de méthode correspondant à la vue, le contrôleur par défaut est
appelé. Ce contrôleur est `Doc::viewDefaultCard`.

### Utilisation des valeurs du document en consultation {#core-ref:f239d142-608b-49a2-b273-0760e78208cf}

Le [contrôleur par défaut][default_view_controleur] fait automatiquement appel
aux méthodes `Doc::viewAttr` et `Doc::viewProp`. Elles initialisent les clés
suivantes :

*   viewAttr va créer :
    *   `L_ATTRID` pour chaque attribut : le libellé (traduit) de l'attribut,
    *   `V_ATTRID` pour chaque attribut : la valeur (au format html) de
        l'attribut,
    *   `S_ATTRID` pour chaque attribut : `true` si l'attribut est vide, `false`
        sinon
*   viewProp va créer :
    *   `ATTRID` pour chaque attribut : la valeur brute de l'attribut
    *   `PROPID` pour chaque propriété : la valeur brute de la propriété
    *   `V_TITLE` une ancre vers le document lui-même avec son titre

**Note** : Toutes ces clefs sont en majuscules.

Lors de l'utilisation d'un contrôleur personnalisé, il est possible d'appeler
ces méthodes afin de générer les clés correspondantes. Il est également possible
de définir d'autres clés en utilisant les différentes méthodes du `Layout`.

**Attention** : Toutes ces clés respectent les visibilités : si la visibilité 
d'un attribut est `H` pour un utilisateur, les clés `L_ATTRID` et `V_ATTRID` 
seront des chaînes vides. `S_ATTRID`, pour sa part, n'est pas affecté par les
visibilités.

## Spécificités du système de template pour les vues openDocument text {#core-ref:3742b35d-ddc0-440e-a0aa-08ea2faf0e46}

Bien que la syntaxe soit très proche de celle des
[vues textuelles][textual_views_syntax], il y a quelques différences à prendre
en compte.

Ces différences sont liées à la structuration des documents odt, qui sont en
fait des documents xml, et dont la structure doit rester valide.

Parmi ces différences, il y a notamment :

*   Les balises `ZONE` ne sont pas prises en compte.
*   Les balises `BLOCK` et `ENDBLOCK` ne sont pas prises en compte et la gestion
    des éléments répétables se fait de [manière spécifique][repetables]
    
    En effet, la notion de *répétable* existe au sein des documents *odt* sous
    la forme des
    *   listes à puce
    *   tableaux
*   La gestion des images se fait de [manière spécifique][images]

### Images {#core-ref:d1625c57-57f6-48eb-ab3e-e3690dddec6c}

Pour incorporer des images, il faut

1.  insérer une image quelconque dans le fichier, au moyen du menu
    <span class="menu"><span class="menu-item">Insertion</span>
    <span class="menu-item">Image</span>
    <span class="menu-item">À partir d'un fichier</span></span>.
    
2.  cliquer sur le menu contextuel de l'image et choisir
    <span class="menu"><span class="menu-item">image</span></span>
    
3.  renseigner la clé dans l'onglet *[Options]*, champ *nom*.
    
    ![ nom de l'image ](representations/odt_insert_image.png)

En ce qui concerne la taille de l'image, la largeur sera conservée.
La hauteur sera calculée en fonction du ratio de l'image dynacase.

**Attention** :chaque image doit être insérée de cette façon, et il ne faut
surtout pas faire de copier coller d'une image. En effet, en cas de copier
coller, les 2 images font référence en interne à la même image, même en
définissant des *noms* différents.

### Répétables {#core-ref:9287cbe8-a6ca-41f9-9547-b7a970ae6584}

La gestion des éléments multiples est intrinsèque à la structure d'un fichier
odt : les listes et tableaux sont multiples par nature. Aussi, utiliser la clé
d'un attribut multiple dans une liste ou un tableau va automatiquement insérer
le nombre d'éléments nécessaire.

Ainsi, par exemple, le template :
![ template ](representations/odt_repetable_source.png)

pourra donner le fichier :
![ résultat ](representations/odt_repetable_resultat.png)

### Conditions {#core-ref:5b53867d-7fb2-4aff-b4dc-941b7d0254b4}

Les conditions (`[IF]` / `[ENDIF]`) sont utilisables, à condition de respecter
la structure du document (Un fichier ODT étant, en interne, un XML, ce fichier
doit conserver son intégrité).

Aussi, les balises ouvrante et fermante doivent être au même niveau. Par
exemple, on ne peut pas mettre un IF au milieu d'un tableau et le ENDIF à
l'extérieur du tableau : le IF et le ENDIF doivent être dans la même cellule du
tableau. Il est possible de les utiliser dans le même paragraphe ou entre
plusieurs paragraphes de même niveau.

En cas d'erreur de structure, un message d'erreur apparaîtra lors de la
consultation du document généré :
![ Erreur de structure ](representations/odt_structure_error.png)

### attributs *htmltext* {#core-ref:9d0e5de3-6176-4b75-aeaa-4b78f0d0a62d}

Le type *htmltext* implique des restrictions d'usage : La valeur de l'attribut
est filtrée lors de l'incorporation dans un fichier openDocument. Seules
certaines balises HTML sont supportées. Les balises non supportées sont ignorées
et non affichées.<span class="fixme" data-assignedto="EBR">ce qui est ignoré, c'est la balise, ou son contenu?</span>

Les balises supportées sont :

| balise HTML | balise ODT         | description                                | restriction                                                                                                                                                                                                                                                                                                       |
| :---------- | :----------------- | :-------------------------------------     | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `p`         | `text:p`           | Insère un paragraphe                       | La balise "&lt;p>" doit être au premier niveau.                                                                                                                                                                                                                                                                   |
| `em/i`      | `text:span`        | Insèrent un texte avec le style "italique" | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `strong/b`  | `text:span`        | Insèrent un texte avec le style "gras"     | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `u`         | `text:span`        | Insère un texte avec le style "souligné"   | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `sup`       | `text:span`        | Insère un texte avec le style "exposant"   | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `sub`       | `text:span`        | Insère un texte avec le style "index"      | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `a`         | `text:a`           | Insère un hyperlien                        | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `h1`        | `text:h`           | Insère un titre de niveau 1                | Le style du texte sera celui de "Titre 1"                                                                                                                                                                                                                                                                         |
| `h2`        | `text:h`           | Insère un titre de niveau 2                | Le style du texte sera celui de "Titre 2"                                                                                                                                                                                                                                                                         |
| `h3`        | `text:h`           | Insère un titre de niveau 3                | Le style du texte sera celui de "Titre 3"                                                                                                                                                                                                                                                                         |
| `h4`        | `text:h`           | Insère un titre de niveau 4                | Le style du texte sera celui de "Titre 4"                                                                                                                                                                                                                                                                         |
| `li`        | `text:lisr`        | Insère une liste à puces numérotée         | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `ul`        | `text:lisr`        | Insère une liste à puces non numérotée     | Doit être dans une balise &lt;p>                                                                                                                                                                                                                                                                                  |
| `table`     | `table:table`      | Insère un tableau                          |                                                                                                                                                                                                                                                                                                                   |
| `tr`        | `table:table-row`  | Insère une rangée tableau                  |                                                                                                                                                                                                                                                                                                                   |
| `th`        | `table:table-cell` | Insère une cellule entête de               |                                                                                                                                                                                                                                                                                                                   |
| `td`        | `table:table-cell` | Insère une cellule tableau                 |                                                                                                                                                                                                                                                                                                                   |
| `img`       | `draw:frame`       | Insère une image                           | L'url de cette image doit être absolue et accessible depuis l'éditeur de texte. Seules les images présente sur les paragraphes de premier niveau sont prises en compte. Pas d'image dans les cellule de tableau. La taille n'est pas configurable. C'est la taille d'origine de l'image qui sera prise en compte. |

<span class="fixme" data-assignedto="EBR">que deviennent les div ? span ? ol ?</span>
<span class="fixme" data-assignedto="EBR">li et ul -> lisr ?</span>

Une clef correspondant à un attribut *htmltext* doit être placée seule dans le
paragraphe, et ne doit pas contenir de texte autour.

### Limitations {#core-ref:b2f63c3f-9f26-47f6-8172-00c23b6a9948}

#### Limitation pour les attributs de type Htmltext {#core-ref:989af790-e851-42f2-b18d-cf5384ba1253}

*   Les couleurs, police, taille de police ne sont pas prises en compte.
*   Pour la mise en forme, seuls les mises en gras, souligné et en italique sont
    supportées.
*   Seuls les titres de niveau 1 à 4 sont pris en compte.
*   Lors de l'utilisation dans une liste, les tableaux ne sont pas interprétés
    et sont traités comme du texte brut.
*   Un attribut htmltext ne peut pas être utilisé dans les entêtes et pied de
    pages.
*   Un attribut htmltext ne peut pas être utilisé dans les propriétés du
    document.
*   Les styles (css) ne sont pas pris en compte.
*   Les imbrications de paragraphes
    (exemple :&lt;p>Texte&lt;p>Texte&lt;/p>&lt;/p>) faites avec des balises
    div, p ou span (ou toutes autres balises de texte) ne sont pas supportées.
    <span class="fixme" data-assignedto="EBR">ca veut dire quoi? (le html de l'exemple n'est pas valide…)</span>

#### Limitations pour les répétables {#core-ref:49c08a3f-c112-497b-9272-d5753f292113}

*   Les répétables ne sont pas gérés dans les entêtes et pied de pages.
*   Les répétables ne sont pas gérés dans les propriétés du document.
*   Les mots-clefs BLOCK/ENDBLOCK ne sont pas gérés.
*   Les listes ne peuvent pas avoir plusieurs niveaux d'imbrication.

#### Limitations pour les relations {#core-ref:d3ca2d74-64dd-4e15-9c84-686515ffc8cb}

*   Les relations de document sont partiellement gérées :
    seul le titre du document est affiché (sans lien).

#### Autres limitations {#core-ref:02b246f0-1c2b-4ef9-8aeb-735ad26ecf3f}

*   Les zones (ZONE) ne sont pas gérés.
*   Les attributs de type fichier, couleur ne sont pas gérés.

## Utilisation avancée {#core-ref:37462ff7-e03a-4fde-99a8-cafb6cedf721}

L'utilisation d'un contrôleur spécifique ainsi que les manipulations avancées
sont détaillées dans la [partie avancée sur les vues OpenDocument
Text][advanced_odt]

<!-- links -->
[TE]: #FIXME
[default_view_controleur]: #core-ref:303fbb4d-a688-4fd7-8329-bbc799251889
[textual_views_syntax]: #core-ref:5f4a2f4b-9ceb-42db-8ac1-2a7baa621ce2
[images]: #core-ref:d1625c57-57f6-48eb-ab3e-e3690dddec6c
[repetables]: #core-ref:9287cbe8-a6ca-41f9-9547-b7a970ae6584
[advanced_odt]: #core-ref:a8c2d27a-6490-4449-9997-2984613ed219