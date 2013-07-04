# Doc::getDocAnchor() {#core-ref:55e9c46c-2a10-4911-8243-7c913416648f}

<div class="short-description">
Générer un fragment HTML contenant une ancre HTML vers un document.
</div>

## Description {#core-ref:8ca28abd-366b-47b8-bf17-9d9e2e952080}

    [php]
    string getDocAnchor ( int $id, 
                       string $target = "_self" ,
                         bool $htmllink = true ,
                  bool|string $title = false ,
                         bool $js = true ,
                       string $docrev = "latest" ,
                         bool $viewIcon = false  )

Permet de générer un fragment HTML, qui pourra être inséré dans un document
HTML, et qui contiendra une ancre HTML (`<a href="…">…</a>`) vers un document
Dynacase.

### Avertissements {#core-ref:124fbf30-ae8c-4dd7-9023-76b80d7804bb}

Aucun.

## Liste des paramètres {#core-ref:de6252d4-d376-4c35-a85d-f2ff835aa224}

(int) `id`
:   L'identifiant du document pour lequel on souhaite générer le code de l'ancre
    HTML.

(string) `target`
:   Le nom du format du lien HTML. Les valeurs supportés sont :
    
    *   **`_self` (par défaut)**,
    
    *   `mail` (pour un fragment HTML inséré dans un mail)
        
        Dans ce cas, l'URL de l'ancre est composée à partir de la valeur du
        [paramètre `CORE_MAILACTIONURL`][CORE_MAILACTIONURL], lui-même composé
        à partir du [paramètre `CORE_MAILACTION`][CORE_MAILACTION].
        
        Cela permet d'effectuer des opérations spécifiques lorsqu'un document
        est accédé depuis un mail.
        
    *   `ext` (pour un fragment HTML inséré dans une interface ExtJS),
    
    toute autre valeur sera prise en compte comme la propriété `target` de
    l'ancre HTML générée.

(bool) `htmllink`
:   Si `false` alors seul le fragment HTML contenant le titre,
    sans ancre, sera généré.

(bool|string) `title`
:   Si une chaîne est spécifiée, alors elle sera utilisée à
    la place du titre du document.

(bool) `js`
:   Si `true` alors du code JavaScript est inclus pour ouvrir le
    document dans une popup.

(string) `docrev`
:   Indique sur quelle révision du document pointera l'ancre HTML.
    
    Les valeurs possibles  sont :
    
    *   `latest`,
    *   `fixed`,
    *   `state(<state>)`.
    
    Se reporter à l'[option `docrev` des attributs docid][docrev] pour plus de
    précisions.

(bool) `viewIcon`
:   Si `true` l'icône de la famille du document sera présentée
    dans l'ancre HTML.

## Valeur de retour {#core-ref:c812a822-8874-49a4-8905-5cc88d2f6eda}

La méthode retourne une chaîne contenant un fragment HTML avec une ancre
vers le document.

## Erreurs / Exceptions {#core-ref:d21f852c-d233-408f-aaeb-ff3cca310d4b}

Aucun.

## Historique {#core-ref:3a513f2a-6956-4199-b716-7919790b3d47}

Aucun.

## Exemples {#core-ref:6167c555-8387-460e-bed6-121a67c2bdd8}

    [php]
    /* Générer une ancre HTML sans JS mais avec l'icône de la famille du document */
    $htmlAnchor = $this->getDocAnchor($docId, "_self", true, false, false, "latest", true);
    
    /* Insérer le fragment HTML dans le layout */
    $this->lay->set('LINK_TO_DOCUMENT', $htmlAnchor);

## Notes {#core-ref:a3c9ae9e-3ed8-4611-9b39-7f742e381d9a}

Aucun.

## Voir aussi {#core-ref:58c61a64-7a4e-4283-9cc1-237fa2b3911d}

Aucun.

<!-- links -->
[docrev]: #core-ref:9bcfd205-fb07-4a71-be06-ba07d4a9cc7c
[CORE_MAILACTION]: #core-ref:c1d9e009-49a5-47a4-9104-4d044ea24aa3
[CORE_MAILACTIONURL]: #core-ref:033299c3-fe9a-4833-9dbd-45952bdf63bc