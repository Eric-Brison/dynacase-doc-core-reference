# Les Zones {#core-ref:7b8214ed-8114-4be0-a2be-9058f5f7c883}

Une zone est un morceau d'IHM. Elle est composée de :

*   un fichier de template, définissant la structure,
*   une fonction php définissant les valeurs.

Par convention :

*   le fichier de template porte l'extension xml,
*   son nom détermine le nom de la zone,
*   la fonction php doit être dans un fichier du même nom,
*   la fonction associée doit porter le même nom. Elle recevra en
    paramètre un objet de la classe `Action` dont la propriété `lay` est
    un objet `Layout`.

<span class="fixme" data-assignedto="EBR">préciser les règles de casse</span>

## Aperçu du système de template {#core-ref:9f10e2bb-b004-418b-8a74-7f155eeef27b}

Le mécanisme de template utilisé dans Dynacase utilise des placeholders de la
forme `[keyword]`.

### Valeurs *atomiques* {#core-ref:e63c75ad-98b5-48b3-a2cb-027392b9b403}

Elles sont définies au moyen de la méthode `Layout::set`. Par exemple :

Le template `atomic.xml` :

    La somme de [X] + [Y] = [XplusY]
    Le produit de [X] * [Y] = [XfoisY]

Associé au fichier `atomic.php` :

    [php]
    function atomic(Action &$action){
        $lay = $action->lay;
        $x=34;
        $y=78;
        $lay->set("X",$x);
        $lay->set("Y",$y);
        $lay->set("XplusY",$x+$y);
        $lay->set("XfoisY",$x*$y);
    }

Donne :

    La somme de 34 + 78 = 112
    Le produit de 34 * 78 = 2652

### valeurs *multiples* {#core-ref:b0f5c7ed-8146-446f-912a-41add1f48dcb}

Elles sont définies au moyen de la méthode `Layout::setBlockData`. Par exemple :

Le template `multiplication.xml` :

    Table de multiplication de [X]
    [BLOCK MUL]
    - [X] * [Y] = [XfoisY][ENDBLOCK MUL]

Associé au fichier `multiplication.php` :

    [php]
    function multiplication(Action &$action){
        $lay = $action->lay;
        $x=3;
        $tmul = array(); // tableau pour le bloc MUL
        
        for ($i=1; $i<10; $i++) {
            $tmul[] = array(
                "Y"      => $i,
                "XfoisY" => $i*$x
            );
        }
        
        $lay->set("X",$x);
        $lay->setBlockData("MUL",$tmul);
    }

Donne :

    Table de multiplication de 3
    
    - 3 * 1 = 3
    - 3 * 2 = 6
    - 3 * 3 = 9
    - 3 * 4 = 12
    - 3 * 5 = 15
    - 3 * 6 = 18
    - 3 * 7 = 21
    - 3 * 8 = 24
    - 3 * 9 = 27
    - 3 * 10 = 30

### Conditions {#core-ref:d3d70fac-d336-4217-b787-fb9937a20f6f}

Elles sont définies  au moyen de la méthode `Layout::set`. Par exemple :

Le template `cond.xml` :

    [text]
    [IF Interdit]Interdit is true[ENDIF Interdit]
    [IFNOT Interdit]Interdit is false[ENDIF Interdit]

Associé au fichier `cond.php` :

    [php]
    function cond(Action &$action){
        $lay = $action->lay;
        $lay->set("Interdit",false);
    }

Donne :

    Interdit is false

### Internationalisation {#core-ref:531cddb2-4523-4409-b092-5a9724acb684}

Pour rendre du texte traduisible, il faut utiliser la syntaxe
`[TEXT:translate me]`. ce texte sera automatiquement ajouté au catalogue de
traduction, et sera remplacé lors du rendu du template.

### Imbrication de templates {#core-ref:200c77c5-2582-43ac-8ff4-2856f902d516}

Il est possible d'appeler un template au sein d'un autre template au moyen de la
syntaxe `[ZONE APP:MY_ZONE]` référençant alors la zone `MY_ZONE` de
l'application `APP`.

## Paramètres de zone {#core-ref:c85b9580-e388-4ff8-a731-3235d68ca27f}

Lors de l'appel d'une zone, avec la notation `APP:MY_ZONE`, il est possible de
spécifier des paramètres, au moyen de la syntaxe `?key1=value1&key2=value2…`.
Par exemple, `APP:MY_ZONE?title=foo&organism=bar`.

Ces paramètres peuvent être récupérés dans la fonction php associée à la zone au
moyen de la classe `ActionUsage`.

<span class="fixme" data-assignedto="MCO">Ajouter un exemple</span>