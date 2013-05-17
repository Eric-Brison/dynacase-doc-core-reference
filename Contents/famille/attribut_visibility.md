# Visibilité des attributs {#core-ref:3e67d45e-1fed-446d-82b5-ba941addc7e8}

Les attributs sont caractérisés par leur visibilité. Cette visibilité indique
si l'attribut est présenté, et s'il est modifiable dans les interfaces. Les différentes
visibilités disponibles sont les suivantes :

`H`
:   Attribut caché : présent dans la dom, il ne sera pas affiché.

`I`
:   Attribut invisible : cet attribut n'est accessible ni par l'IHM, ni par le
    code (pour le modifier par le code, il faut au préalable modifier
    explicitement sa visibilité).

`O`
:   Attribut visible en *modification* uniquement, et modifiable.

`R`
:   Attribut visible uniquement en *consultation*.

`S`
:   Attribut visible en *consultation* et en *modification*, mais non modifiable.

`U` (**applicable uniquement au type *array***)
:   Array affiché en *consultation* et en *modification*, mais dont le nombre de
    lignes ne peut pas être modifié.

`W`
:   Attribut visible en *consultation* et en *modification*, et modifiable

Il est important de distinguer la visibilité et les droits. **La visibilité n'offre pas de protection contre l'accès à l'information** sauf pour la visibilité `I`.


## Visibilité des attributs structurants {#core-ref:8349d1e6-ad9b-4c51-957e-b3f63497354c}

Les visibilités des attributs structurants impactent celle des attributs qu'ils
contiennent. Ainsi, par exemple, un attribut `W` dans un cadre `H` sera en fait
en `H`. Voici la table qui récapitule ces cas :

| Attribut structurant     | Attribut | Visibilité résultante |
| :-                     : | :      : | :                   : |
| `H`                      | `H`      | `H`                   |
| `H`                      | `I`      | `I`                   |
| `H`                      | `O`      | `H`                   |
| `H`                      | `R`      | `H`                   |
| `H`                      | `S`      | `H`                   |
| `H`                      | `U`      | `H`                   |
| `H`                      | `W`      | `H`                   |
| `I`                      | `H`      | `I`                   |
| `I`                      | `I`      | `I`                   |
| `I`                      | `O`      | `I`                   |
| `I`                      | `R`      | `I`                   |
| `I`                      | `S`      | `I`                   |
| `I`                      | `U`      | `I`                   |
| `I`                      | `W`      | `I`                   |
| `O`                      | `H`      | `H`                   |
| `O`                      | `I`      | `I`                   |
| `O`                      | `O`      | `O`                   |
| `O`                      | `R`      | `R`                   |
| `O`                      | `S`      | `S`                   |
| `O`                      | `U`      | `U`                   |
| `O`                      | `W`      | `O`                   |
| `R`                      | `H`      | `H`                   |
| `R`                      | `I`      | `I`                   |
| `R`                      | `O`      | `R`                   |
| `R`                      | `R`      | `R`                   |
| `R`                      | `S`      | `R`                   |
| `R`                      | `U`      | `R`                   |
| `R`                      | `W`      | `R`                   |
| `S`                      | `H`      | `H`                   |
| `S`                      | `I`      | `I`                   |
| `S`                      | `O`      | `O`                   |
| `S`                      | `R`      | `R`                   |
| `S`                      | `S`      | `S`                   |
| `S`                      | `U`      | `U`                   |
| `S`                      | `W`      | `S`                   |
| `W`                      | `H`      | `H`                   |
| `W`                      | `I`      | `I`                   |
| `W`                      | `O`      | `O`                   |
| `W`                      | `R`      | `R`                   |
| `W`                      | `S`      | `S`                   |
| `W`                      | `U`      | `U`                   |
| `W`                      | `W`      | `W`                   |

Les tableaux en visibilité `U` sont *transparents* lors de cette propagation.
Pour les attributs contenus dans un tableau en visibilité `U`, il faut donc
regarder l'attribut structurant du-dit tableau.