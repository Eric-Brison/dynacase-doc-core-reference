# API pour l'utilisation des notifications


## Envoi d'événements

Un événement est constitué de :

*   name
:   un nom : ce nom n'est pas unique - il permet d'identifier l'événement et sert 
    de correspondance avec l'écouteur

*   data 
:   des données utilisables dans le cadre du traitement de l'événement.
    Ces données peuvent être de tout type supportant une sérialisation (pas de type
    resource ou closure par exemple).

*   context
:   un ensemble de critère "simple" permettant à l'écouteur de filtrer l'événement à écouter.
    Ces critères sont une liste de clef/valeur. Les clefs et les valeurs sont de simples chaînes
    de caractères.

Méthodes permettant d'initialiser un événement.

    [php]
    /**
     * @param string $name event name
     */
    public function __construct($name);
    
    /**
     * add a new data in event
     * @param string $key
     * @param mixed $value
     */
    public function addData($key, $value);
    
    /**
     * add new criteria
     * @param string $key
     * @param string $value
     */
    public function addContext($key, $value);

## Abonnement 

Un abonnement est constitué de :

*   id
    Un identifiant unique

*   eventNames
    Un ou plusieurs nom d'événement à écouter (possibilité aussi d'utiliser '*')

*   data
:   des données utilisables dans le cadre du traitement de l'événement.
    Ces données peuvent être de tout type supportant une sérialisation.

*   criteria
:   des données de correspondances (clef/valeur). Ces clefs permettent de vérifier
    que le contexte de l'événement correspond. Pour correspondre, il faut que
    le contexte de l'événement contienne toutes les clefs/valeurs définies dans les
    critères.

*   callback
:   méthode devant être appelé lorsqu'un événement correspondant est détecté.
    Cette méthode doit être "statique". L'événement est passé en paramètre 
    de la méthode.

Méthodes permettant d'initialiser un écouteur.


    [php]
    /**
     * @param string|string[] $eventName event name(s) to listen
     */
    public function __construct($eventName);
    
     /**
     * @param string|string[] $eventName event name to listen
     */
    public function assertEventTypeMatch($type);
    
    /**
     * @param string $code unique id
     */
    public function setUniqueId($code)
    
    /**
     * add data to be use in process
     * @param string $key
     * @param mixed $value
     */
    public function addData($key, $value);
    
    /**
     * Add criteria to match event's contexte
     * @param string $key
     * @param string $value
     */
    public function addCriteria($key,  $value)
    
    /**
     * Method to call when event is processed
     * @param string $method
     */
    public function attach($method) {

## Manager

Le gestionnaire d'événement a en charge de réaliser l'envoi des événements et le 
traitement des événements.

    [php]
    /**
     * add a new listener
     * @param CoreEventListener $l
     * @return string listener identifier
     */
    public static function addListener(CoreEventListener $l)
    
    /**
     * delete a indetified listener
     * @param string $listenerId
     */
    public static function deleteListener($listenerId);
    
    /**
     * delete all listener which listen a eventName
     * If a listener has several eventName matching, only the matching are removed. 
     * The listener is removed if as no more matching event.
     * @param string $eventName
     */
    public static function deleteListenerMatchingEvent($eventName);
    
    /**
     * if listener identifier is already recorded, the listener is updated
     * else a new listener is recorded 
     * @param CoreEventListener $l
     * @return string listener identifier
     */
    public static function addOrUpdateListener(CoreEventListener $l)
    
    /**
     * Send event to be processed
     * @param CoreEvent $e
     */
    public static function dispatch(CoreEvent $e)
    
    /**
     * indicate that no dispatch will be effective in next code
     * @param bool $stop stop or unstop propagation
     */
    public function stopPropagation($stop=true) {
        
    }

## Spécialisation sur les documents

### Événement sur un document

    [php]
    class DocEvent extends CoreEvent


Cette classe héritant des événements de base initialise son contexte avec les
éléments suivants :

*   `doc.initid` : identifiant initial du document
*   `doc.name` :   nom logique du document
*   `doc.id` :  identifiant du document
*   `doc.fromname` : nom de la famille
*   `doc.updateValues` : retour de Doc::getOldRawValues() au moment de l'envoi.

Les données ajoutés sont les mêmes que les critères.

Méthodes ajoutées :

    [php]
    /**
     * get document in last revision
     * @return  \Doc
     */
    public function getTargetDocument();
    
    /**
     * get modified attributes values when event has been send
     * @return  array
     */
    public function getOldRawValues()

Cette méthode permet de récupérer le document à l'origine de l'événement.

Nécessite d'être utilisé avec `DocEventManager::dispatch()`. `DocEventManager`
est  une classe (héroté de EventManager) spécialisée dans le traitement des
`DocEvent`.

### Abonnement sur un document particulier

    [php]
    class DocEventListener extends CoreEventListener

Méthodes ajoutées :

    [php]
    /**
     * Document method call when event is processed
     * @param string $methodCall
     */
    public function setCallBackMethod($methodCall);
    
    /**
     * To match only one document 
     * @param string $attrid attribute identifier
     */
    public function assertTargetInitidEquals($attrid)
    
    /**
     * set one or several fromname to match
     * @param string|string[] $fromnames
     */
    public function assertTargetFromNameMatch($fromnames) 
    
     /**
     * assert values of relations attributes
     * @param string[] $attrid
     */
    public function assertTargetInitidIsIncludedIn(array $attrid);
    
    /**
     * add several docid to match event
     * @param int[] $docids
     */
    public function assertTargetInitidIn(array $docids)

Nécessite d'être utilisé avec `DocEventManager`.



### Abonnement sur une famille


    [php]
    class FamilyEventListener extends DocEventListener

Méthode redéfinie :

    [php]
     /**
     * assert values of relations attributes
     * @param string[] $attrid
     */
    public function assertTargetInitidIsIncludedIn(array $attrid);
    
    public function assertTargetInitidEqualsToAttribute($attrid)

Pour ces 2 méthodes, ce sont les noms des attributs qui serviront à filtrer lors
du déclenchement de la notification et non les valeurs comme pour le document.

Nouvelles méthodes :

    [php]
    /**
     * Family document to inspect
     * @param string $familyName
     */
    public function setFamily($familyName)

Cette méthode vérifiera les conditions sur tous les documents de la famille 
indiquée.

## Exemples

#### Notification brute

Le nom de l'événement `MyLog` permet de cibler la notification.

    [php]
    // listen
    $l = new \Dcp\CoreEventListener("MyLog");
    $l->attach("LogTest::info()");
    \Dcp\EventManager::addListener($l);


    [php]
    class LogTest
    {
        public static function info(\Dcp\CoreEvent $e)
        {
            error_log($e->getData("text"));
        }
    }

    [php]
    // send event
    $docEvent = new \Dcp\CoreEvent("MyLog");
    $docEvent->addData("text", "hello");
    \Dcp\EventManager::dispatch($docEvent);


Les noms d'événements sur le _listen_ peuvent utiliser le méta-caractères `*`.

    [php]
    $l = new \Dcp\CoreEventListener("MyLog*");

Le caractère `*` se substitue à une suite de caractères quelconques.

Cela correspond à `MyLog` ou `MyLog.special`.




#### Notification sur un document

Ceci envoi une notification de nom `event.core.doc`

Envoi 

    [php]
    $doc=new_doc("", "ZOO_ESP_ALLI");
    $docEvent = new \Dcp\DocEvent(\Dcp\DocEvent::docEventType, $doc);
    \Dcp\DocEventManager::dispatch($docEvent);


Abonnement

    [php]
    $doc=new_doc("", "ANI_THEO");
    $l= new \Dcp\DocEventListener(\Dcp\DocEvent::docEventType, $doc);
    $l->assertTargetInitidEquals("an_espece");//->assertCriteria("initid", $doc->getRawValue("an_espece"));
    \Dcp\DocEventManager::dispatch($docEvent);

#### Notification sur une famille

Pose de l'écoute.

    [php]
    $l = new \Dcp\FamilyEventListener(\Dcp\DocEvent::docEventUpdateType, "ZOO_ANIMAL");
    $l->assertTargetFromNameEquals("ZOO_ESPECE"); // vérification que l'événement est sur une espèce
    $l->assertTargetInitidIsIncludedIn("an_espece");
    $l->assertEventTypeMatch(\Dcp\DocEvent::docEventUpdateType); // `event.core.doc.update`
    $l->assertEventClassEqual("Dcp\\DocEvent"); // optionnel: filtre sur la classe de l'événement
    $l->setCallBackMethod("::addHistoryEntry()");
    \Dcp\DocEventManager::addListener($l);

Autre écoute plus générale :


    [php]
    $l = new \Dcp\FamilyEventListener(\Dcp\DocUpdateEvent::docEventUpdateType, "ZOO_ANIMAL");
    $l->assertTargetFromNameMatch(array("ZOO_ESPECE","ZOO_ANIMAL"));
    $l->assertTargetInitidIsIncludedIn(array("an_espece", "an_enfant"));
    $l->setCallBackMethod("::addHistoryEntry()");
    \Dcp\DocEventManager::addListener($l);

Envoi d'un événement de nom `event.core.doc.update` qui sera capté pour les 2
écouteurs décrits ci-dessus.

    [php]
    // send event from espece
    $doc=new_doc("", "ZOO_ESP_ALLI");
    $doc->setValue("es_poids", "123");
    $doc->setValue("es_habitat", "ici");
    $docEvent = new \Dcp\DocEvent(\Dcp\DocEvent::docEventUpdateType, $doc);
    \Dcp\DocEventManager::dispatch($docEvent);

#### Notification sur une modification document

Ceci envoi une notification de nom `event.core.doc.update`


Envoi 

    [php]
    $doc=new_doc("", "ZOO_ESP_ALLI");
    $doc->setValue("es_poids", "123");
    $doc->setValue("es_habitat", "ici");
    $docEvent = new \Dcp\DocEvent(\Dcp\DocEvent::docEventUpdateType, $doc);
    \Dcp\DocEventManager::dispatch($docEvent);



Abonnement

    [php]
    $doc = new_doc("", "ANI_ELEO");
    $l = new \Dcp\DocEventListener(\Dcp\DocUpdateEvent::docEventUpdateType, $doc);
    $l->setCallBackMethod("::addHistoryEntry()");
    $l->assertTargetInitidIn(
        array_merge($doc->getMultipleRawValues("an_enfant"),
        array($doc->getRawValue("an_espece"))));
    \Dcp\DocEventManager::addListener($l);
