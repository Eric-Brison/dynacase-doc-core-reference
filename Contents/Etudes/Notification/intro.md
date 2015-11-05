# Notifications

Le système de notification permet d'envoyer et de s'abonner à des événements
côté serveur. Ces événements sont transmis et reçu de manière asynchrone.

Le but est de simplifier les traitements qui sont liés entre plusieurs documents.

Exemple de problème récurrent :

Un document construit un tableau avec un ensemble de document qui lui sont liés.
Chaque modification d'un document lié impacte le document cible.

Le but est de ne plus utiliser le hook de refresh qu'à des fins de présentation
et non de calcul d'attribut.

Ceci a comme avantage d'améliorer grandement la vitesse de rendu d'un document
et permet de mieux garantir l'idempotence d'un 'GET' sur le document. Dans ce
cas, un cache peut être utilisé.
