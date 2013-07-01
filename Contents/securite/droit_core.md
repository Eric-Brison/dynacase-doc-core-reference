# Droits définis sur les applications fournies par Dynacase Core {#core-ref:b708cfe1-f94c-44eb-9983-8760accf54ff}

<span class="fixme" data-assignedto="EBR">Que veut dire "mis par défaut" ? c'est
le statut pour le groupe `GDEFAULT` ?</span>

| Application | Droit          | Mis pas défaut | Description                                                                                                               |
| ----------- | -------------- | :------------: | ------------------------------------------------------------------------------------------------------------------------- |
| FDL         | EDIT           | Oui            | Autorise le verrouillage et le déverrouillage de document. Accès aux menus spécifiques liés au méthodes du document       |
| FDL         | NORMAL         | Oui            | Autorise les accès aux interfaces standards de consultation de document                                                   |
|             |                |                |                                                                                                                           |
| FDL         | SYSTEM         | Non            | Autorise la modification des paramètres pour les documents famille. Doit être utilisé en corrélation avec FREEDOM_MASTER. |
| FDL         | FAMILOui       | Non            | Autorise le paramétrage spécifique de famille.                                                                            |
| FDL         | EXPORT         | Non            | Autorise l'exportation de dossiers ou de recherches. Doit être utilisé en corrélation avec FREEDOM_MASTER.                |
|             |                |                |                                                                                                                           |
| GENERIC     | GENERIC_READ   | Oui            | Autorise les accès aux interfaces standards de liste de documents                                                         |
| GENERIC     | GENERIC        | Oui            | Autorise les accès aux interfaces standards de modification de document                                                   |
| GENERIC     | GENERIC_MASTER | Non            | Autorise les accès aux interfaces d'importation par famille et au contrôle des énumérés                                   |
|             |                |                |                                                                                                                           |
| FREEDOM     | FREEDOM_HISTO  | Oui            | Autorise la consultation de l'historique du document                                                                      |
| FREEDOM     | FREEDOM_READ   | Oui            | Accès aux interfaces de consultation de l'application FREEDOM (liste de document, arborescence de dossier)                |
| FREEDOM     | FREEDOM        | Oui            | Accès aux interfaces de modification (déplacement de dossier, duplication, ...)                                           |
| FREEDOM     | FREEDOM_ADMIN  | Non            | Accès aux interfaces de traitement par lot                                                                                |
| FREEDOM     | FREEDOM_MASTER | Non            | Accès aux interfaces d'importation et d'exportation.                                                                      |
|             |                |                |                                                                                                                           |
| FGSEARCH    | FGSEARCH_READ  | Oui            | Accès à la recherche générale                                                                                             |
|             |                |                |                                                                                                                           |
| DAV         | DAV_USER       | Oui            | Accès à l'espace d'échange de fichiers via le protocole WebDav. (non configuré par défaut)                                |
