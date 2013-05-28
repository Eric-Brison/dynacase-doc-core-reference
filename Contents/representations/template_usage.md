# Utilisation des templates {#core-ref:5f4a2f4b-9ceb-42db-8ac1-2a7baa621ce2}

Les templates utilisés pour les vues de documents sont gérés par la
[classe `Layout`][advancedtemplate]. Cette classe permet de renseigner des
parties variables définies dans un fichier texte.

Le mécanisme de template utilisé dans Dynacase utilise des placeholders de la
forme `[keyword]`.

## Valeurs *atomiques*  {#core-ref:4fdd120b-eaf1-4fbf-a157-f4eb3ee62e76}

Elles sont définies au moyen de la méthode `Layout::set`. Par exemple :

Le template `atomic.xml` :

    La somme de [X] + [Y] = [XplusY]
    Le produit de [X] * [Y] = [XfoisY]

Associé au fichier `atomic.php` :

    [php]
    
        $lay = new Layout("atomic.xml");
        $x=34;
        $y=78;
        $lay->set("X",$x);
        $lay->set("Y",$y);
        $lay->set("XplusY",$x+$y);
        $lay->set("XfoisY",$x*$y);
        print $lay->gen();
    

Donne :

    La somme de 34 + 78 = 112
    Le produit de 34 * 78 = 2652

## valeurs *multiples*  {#core-ref:587b563e-7371-469f-9d1e-350607056c73}

Elles sont définies au moyen de la méthode `Layout::setBlockData`. Par exemple :

Le template `multiplication.xml` :

    Table de multiplication de [X]
    [BLOCK MUL]
    - [X] * [Y] = [XfoisY][ENDBLOCK MUL]

Associé au fichier `multiplication.php` :

    [php]
    
        $lay = new Layout("multiplication.xml");
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
        print $lay->gen();
    

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

## Conditions  {#core-ref:ecf5bdf3-3d61-4c59-b640-4a62dc2054c5}

Elles sont définies  au moyen de la méthode `Layout::set`. Par exemple :

Le template `cond.xml` :

    [text]
    [IF Interdit]Interdit is true[ENDIF Interdit]
    [IFNOT Interdit]Interdit is false[ENDIF Interdit]

Associé au fichier `cond.php` :

    [php]
    
        $lay = new Layout("cond.xml");
        $lay->set("Interdit",false);
    

Donne :

    Interdit is false

## Internationalisation  {#core-ref:6a4b3a9b-11b6-47d4-b387-0ff177dd9f82}

Pour rendre du texte traduisible, il faut utiliser la syntaxe
`[TEXT:translate me]`. ce texte sera automatiquement ajouté au catalogue de
traduction, et sera remplacé par sa traduction lors du rendu du template.



<!-- links -->
[advancedtemplate]: #core-ref:af9ea76c-069e-49e1-a382-efc8ca35f1eb