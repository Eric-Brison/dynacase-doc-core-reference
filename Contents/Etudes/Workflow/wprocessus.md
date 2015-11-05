# Workflow de processus

Le workflow de processus se distingue du workflow de document par la fait qu'il ne
s'applique pas à un document en particulier.


Ce mécanisme permet de suivre des cycles (passage de transition) comme le cycle
de document mais les actions de ce cycle peuvent impliquer de 0 à n documents.
Ces documents pouvant eux-aussi être soumis à des workflow de document.


La norme [BPMN][BPMN] est une norme de définition de ce type de workflow.

Deux possibilités s'offre à nous :

1.  Donner les moyen de s'interfacer avec un outils de gestion de processus existant
2.  Implémenter nous-même, une gestion de ce type de processus.


[BPMN]: https://camunda.org/bpmn/tutorial/