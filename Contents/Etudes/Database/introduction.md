# La base de données 

La base de données nécessite une réorganisation afin de supporter de plus grand
volumes de données.

Le but est de pouvoir plus facilement dédier des partitions disques différentes 
entre les données de recherches et les données de productions.

De plus, les attributs multivalué (et par conséquent les tableaux) ne sont pas
typés et ne peuvent pas faire l'objet de recherche efficace. C'est pourquoi,
l'usage des tableaux postgresql est envisagé pour pouvoir bénéficier d'opérateur 
plus spécialisés et plus rapides.


Il est aussi nécessaire de normaliser les paramétrages qui enregistrent une
structure comme par exemple les valeurs de paramètres, les valeurs par défaut,
etc. La structure "jsonb" (dispo en PG9.4) semble être un bon candidat comme
type de donnée.

Le but est de ne plus avoir de syntaxe spécifique et d'utiliser que des
standards fournis par le base de données.
