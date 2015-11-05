# Sécurité au niveau des attributs

Par contre l'accès en lecture ou écriture des attributs n'est pas soumis à des droits
particulier.

Il faut remplacer la notion de "visibility" donnée dans la structure de la
famille par la notion d'accès.

*   RO : Read only
*   WO : Write only
*   RW : Read Write
*   NA : No access (no read, no write)

La visibilité étant déduite de l'accès. Celle-ci pouvant être modifiée le cas
échéant par la configuration de rendu.

Ce contrôle d'accès est controlé au plus bas niveau dans les objets documentaire
(Doc::getValue, Doc::setValue).

La désactivation de ce contrôle pourra être levé. En ce qui concerne cette
désactivation de contrôle, une fonction de type "sudo" peux être envisagée afin
simplifier les contraintes du à ce contrôle supplémentaire.