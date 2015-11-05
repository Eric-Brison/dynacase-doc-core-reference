# Définition de requêtes complexes

La définition de requête pour la recherche de document peut devenir assez vite
limité si on utilise juste des méthodes avec des filtres standard.

Il faut envisager un langage de requêtage plus proche de ce qu'on pourrai faire
avec une requête SQL standard.

La norme [CMIS][CMISsearch] a déjà pensé à ce langage et la normalisé. En fait
c'est une requête proche de la norme SQL92. Un développeur peut alors réaliser
les jointures et les conditions qu'il désire. De notre côté, il faut juste
s'assurer qu'il dispose de manière assez intuitive des tables et des relations
de jointure.

Ce langage peut être utilisé pour paramétrer aussi une requête via l'api REST de
recherche de document.

[CMISsearch]:   http://docs.oasis-open.org/cmis/CMIS/v1.1/os/CMIS-v1.1-os.html#x1-10500014