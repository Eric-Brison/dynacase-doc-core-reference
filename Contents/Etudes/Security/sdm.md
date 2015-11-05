# Sécurité DocManager

Le docManager possède une méthode [getDocument][getDocument]. Il est à délibérer
pour savoir si cette méthode est soumise au droit "voir" du document ou non.

Ce choix pouvant être débatu, il ne me parait pas judicieux de contrôler aussi
les accès aux familles à travers la méthode `getFamily()`.

La fonction "sudo", de toute façon, inhibera les contrôles si elle est appelée.

[getDocument]:       #core-ref:dfa0762f-6ff3-4349-bd21-6442740d9dcc