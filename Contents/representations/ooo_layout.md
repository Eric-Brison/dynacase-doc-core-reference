# Vue OpenDocument Text {#core-ref:d03e0905-2be1-4649-a823-9f64e94cba29}

Une vue openDocument text permet de générer une représentation bureautique du
document. Cette représentation est au format *odt*, et peut être convertie en
*pdf*, ou autre format bureautique, au moyen du [moteur de transformation][TE].

Étant donné que cette représentation est binaire, il y a de nombreuses
différences entre ces représentations et les représentations html.

Il est à noter que les vues openDocument text ne sont utilisables que pour la
consultation.

Une vue OpenDocument Text est composée de :

*   un fichier de template (au format *odt*), définissant la structure,
*   une méthode (appelée contrôleur de vue) du document à représenter,
    définissant les valeurs.  
    Cette méthode peut également être omise. dans ce cas, dynacase fera appel
    au [contrôleur de vue par défaut][default_view_controleur].

<span class="fixme" data-assignedto="EBR">préciser les règles de casse</span>

## Le contrôleur de vue {#core-ref:a7e88a30-c481-4e94-975f-c91c2eb4257d}

Pour qu'une méthode du document soit utilisable en tant que contrôleur d'une
vue, il est nécessaire de lui ajouter la phpDoc `@templateController` afin
de se prémunir d'une éventuelle exécution arbitraire de code.

les paramètres reçus par la méthode sont au nombre de 3 :

*   `$target` (string): nom de la fenêtre graphique qui sera utilisé pour les
    hyperliens (`"_self"` par défaut) ;
*   `$ulink` (booléen) : indique s'il faut générer les hyperliens (`true` par
    défaut) ;
*   `$abstract` (booléen) : indique s'il ne faut pas générer uniquement les
    attributs de la fiche résumé (`false` par défaut).

### Contrôleur par défaut {#core-ref:303fbb4d-a688-4fd7-8329-bbc799251889}

En l'absence de méthode correspondant à la vue, le contrôleur par défaut est
appelé. Ce contrôleur est `Doc::viewDefaultCard`.

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

### Insertion d'images {#core-ref:d1625c57-57f6-48eb-ab3e-e3690dddec6c}

Pour incorporer des images, il faut

1.  insérer une image quelconque dans le fichier, au moyen du menu
    <span class="menu"><span class="menu-item">Insertion</span>
    <span class="menu-item">Image</span>
    <span class="menu-item">À partir d'un fichier</span></span>.
2.  cliquer sur le menu contextuel de l'image et choisir
    <span class="menu"><span class="menu-item">image</span></span>
3.  renseigner la clé dans l'onglet *[Options]*, champ *nom*.

En ce qui concerne la taille de l'image, la largeur sera conservée.
La hauteur sera calculée en fonction du ratio de l'image dynacase.

**Attention** :chaque image doit être insérée de cette façon, et il ne faut
surtout pas faire de copier coller d'une image. En effet, en cas de copier
coller, les 2 images font référence en interne à la même image, même en
définissant des *noms* différents.

### répétables {#core-ref:9287cbe8-a6ca-41f9-9547-b7a970ae6584}

<!-- links -->
[TE]: #FIXME
[default_view_controleur]: #core-ref:303fbb4d-a688-4fd7-8329-bbc799251889
[textual_views_syntax]: #core-ref:5f4a2f4b-9ceb-42db-8ac1-2a7baa621ce2
[images]: #core-ref:d1625c57-57f6-48eb-ab3e-e3690dddec6c
[repetables]: #core-ref:9287cbe8-a6ca-41f9-9547-b7a970ae6584