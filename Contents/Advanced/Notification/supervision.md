# Supervision des notifications

## Log des événéments

Le traitements des événéments produisent des entrées dans une table de log.

EventManager::getLog()

*   idEvent
*   idListener
*   date
*   code
*   message

| idEvent | idListener |           date           |    code    |             message             |
| ------- | ---------- | ------------------------ | ---------- | ------------------------------- |
|      34 |            | 2013-07-14 12:00:54.4568 | RECORD     | [event configuration (json)]    |
|      34 |            | 2013-07-14 12:00:56.768  | PROCESS    |                                 |
|      34 | abc567578  | 2013-07-14 12:00:56.8568 | RUN        | [listener configuration (json)] |
|      34 | abc567578  | 2013-07-14 12:00:56.973  | ENDRUN     | transition active               |
|      35 |            | 2013-07-14 12:00:57.568  | RECORD     | [event configuration (json)]    |
|      34 | fghf456    | 2013-07-14 12:00:57.1568 | RUN        | [listener configuration (json)] |
|      34 | fghf456    | 2013-07-14 12:00:59.473  | ENDRUN     | mail sended to me@some.org      |
|      34 |            | 2013-07-14 12:00:59.583  | ENDPROCESS |                                 |
|      35 |            | 2013-07-14 12:01:00.768  | PROCESS    |                                 |
|      35 | rty67888   | 2013-07-14 12:01:01.4568 | RUN        | [listener configuration (json)] |
|      35 | rty67888   | 2013-07-14 12:01:04.973  | ENDRUN     | document 3657 modified          |
|      35 |            | 2013-07-14 12:01:05.83   | ENDPROCESS |                                 |

EventManager::getListeners()

## Élément de supervision

EventManager::getListeners()
    
*   id
*   type
*   eventName
*   criteria

EventManager::getEvents($statusfilter='')

*   id
*   type
*   context
*   dispatchDate
*   activedDate
*   doneDate
*   matchListeners[]
*   returnedMessage
*   status (new, active, done)
*   returnedErrorMessage


## Paramètres

*   temps de sauvegarde des log 

## Interface d'administration

Affichage du tableau des écoutes.

|  id | type | eventName | criteria |
| --- | ---- | --------- | -------- |

Utilisation d'une datagrid classique avec filtrage sur colonne.



Affichage du tableau des événements.

Ordonné par date et paginé.


|  id | date d'enregistrement | status | durée d'exécution | context | écouteurs utilisés | message | message d'erreur |
| --- | --------------------- | ------ | ----------------- | ------- | ------------------ | ------- | ---------------- |

Si clic sur "id", une popup de détail des caractéristiques de l'événement.
Si clic sur "écouteur", une popup de détail des caractéristiques de l'écouteur.








