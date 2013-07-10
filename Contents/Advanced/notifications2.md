# Notifications (2)

## Use Case 1 (standard) :

Soit les familles Animal et Enclos.

*   Animal possède  
        un attribut an_enclos de type relation vers Enclos  
        un attribut an_enclossurface
*   Enclos possède  
        un attribut en_surface


Lorsque un document de la famille **Enclos** est mis à jour : pour chaque
document Animal dont **an_enclos** référence le document modifié, la valeur de
l’attribut **an_enclossurface** doit être mise à jour avec la valeur de
**en_surface**


### Envoi de la notification


Cette version implique que l'objet `DocEvent` s'occupe de
récupérer les données pour l'utilisation.


Une implémentation de DocEvent donne :

    [php]
    class CoreEvent
    {
        public function __construct($type) {
            
        }
        /**
         * @return  string
         */
        public function getSendDate()
        {
            return date('Y-m-dTh:i:s');
        }
        
        public function addData($key, $value)
        {
        }
        public function getData($key)
        {
            return '';
        }
    }

    [php]
    class DocEvent extends CoreEvent
    {
        const docEventType = "docevent.standard";
        
        public function __construct($type, \Doc $doc)
        {
            parent::__construct($type);
            $this->addData( "initid", $doc->initid);
            $this->addData("id", $doc->id);
            $this->addData("fromname", $doc->fromname);
        }
        /**
         * in last revision
         * @return  \Doc
         */
        public function getDocument()
        {
            return new_Doc("", $this->getData("initid"),true);
        }
        /**
         * in last revision
         * @return  \Doc
         */
        public function getTargetDocument()
        {
            return new \Doc();
        }
        /**
         * in last revision
         * @return  \Doc
         */
        public function getEventDocument()
        {
            return new \Doc();
        }
    }

Ici on spécialise l'objet pour avoir en plus les valeurs modifiées.

    [php]
    class DocEventUpdate extends DocEvent
    {
        const docEventUpdateType = "doceventupdate.standard";
        public function __construct($type, \Doc $doc)
        {
            parent::__construct($type, $doc);
            $this->addData("updateValues", $doc->getOldrawValues());
        }
        /**
         * @return  array
         */
        public function getOldRawValues()
        {
            return $this->getData("updateValues");
        }
    }

Son utilisation dans l'enclos

    [php]
    namespace Zoo;
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    use \Dcp\AttributeIdentifiers\Iuser as Aiuser;
    use Dcp\AttributeIdentifiers as Attribute;
    use Dcp\Events;
    use Dcp\Family as Family;
    
    class Zoo_Enclos extends Family\Document
    {
        public function postStore()
        {
            $err=parent::postStore();
            if (empty($err) && $this->isChanged()) {
                $e = new \Dcp\DocEventUpdate(\Dcp\DocEventUpdate::docEventUpdateType, $this);
                Events::dispatch($e);
            }
            return $err;
        }
    }

### pose de l'écoute 

#### version 1

    [php]
    class Zoo_Animal extends Family\Document
    {
        public function postStore()
        {
            $err = parent::postStore();
            if ($this->isChanged()) {
                // écoute sur l'enclos
                
                // filtre sur les données de l'événement
                $eventFilter = array(
                    sprintf("initid = %d", $this->getAttributeValue(Attribute\Zoo_animal::an_enclos)),
                    sprintf("updateValues @> '%s'", Attribute\Zoo_enclos::en_surface)
                );
                // cela suppose de connaître ici les identifiants des données de l'événement.
                
                $edl = new \Dcp\EventDocListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,// filtre sur le type de l'événement
                    $this, $eventFilter
                );
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->setCallBackMethod("::refreshEnclos()");
                // pose de l'écoute
                Events::addOrUpdateListener($edl );
            }
            return $err;
        }
        
        public function refreshEnclos(\Dcp\DocEventUpdate $e)
        {
            $enclos = $e->getTargetDocument();
            $this->setValue(Attribute\Zoo_animal::an_enclossurface,
                $enclos->getRawValue(Attribute\Zoo_enclos::en_surface));
            if ($this->isChanged()) {
                $this->store();
            }
        }
    }

#### version 2

Le filtre peut être ré-écrit avec des constantes :

Ajout des constantes dans les classes d'événements :

    [php]
    class DocEvent extends CoreEvent
    {
        const docEventType = "docevent.standard";
        
        const dataInitid="initid";
        const dataId="id";
        const dataFromName="fromname";
        public function __construct($type, \Doc $doc)
        {
            parent::__construct($type);
            $this->addData( self::dataInitid, $doc->initid);
            $this->addData(self::dataId, $doc->id);
            $this->addData(self::dataFromName, $doc->fromname);
        }
        //....
    }

    [php]
    class DocEventUpdate extends DocEvent
    {
        const docEventUpdateType = "doceventupdate.standard";
        const dataUpdateValues="updateValues";
        public function __construct($type, \Doc $doc)
        {
            parent::__construct($type, $doc);
            $this->addData(self::docEventUpdateType, $doc->getOldrawValues());
        }
        //...
    }

Ce qui donne le filtre suivant :

    [php]
       $eventFilter = array(
            sprintf("%s = %d", 
                \Dcp\DocEventUpdate::dataInitid, 
                $this->getAttributeValue(Attribute\Zoo_animal::an_enclos)),
            sprintf("%s @> '%s'", 
                 \Dcp\DocEventUpdate::dataUpdateValues, 
                Attribute\Zoo_enclos::en_surface)
        );

#### version 3

Avec des méthodes en plus : plus de filtre explicite


    [php]
       $edl = new \Dcp\EventDocListener(
            \Dcp\DocEventUpdate::docEventUpdateType,
            $this
        );
        
        $edl->assertTargetInitidEquals($this->getAttributeValue(Attribute\Zoo_animal::an_enclos));
        $edl->assertTargetModifiedAttributeIncludes(Attribute\Zoo_enclos::en_surface);
        $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
        $edl->setCallBackMethod("::refreshEnclos()");
        // pose de l'écoute
        Events::addOrUpdateListener($edl );

Un filtre plus général est accessible aussi sur les data :

    [php]
    function assertData($dataName, $operand, $value);
    
Les opérateurs sont une liste finie qui permet de réaliser un filtre sql au final.

    function assertTargetInitidEquals($value) {
        return $this->assertData(\Dcp\DocEventUpdate::dataInitid, "=", $value);
    }

## Use Case 2 (standard) :

Soit les familles Enclos et Espece.

*   Enclos possède  
        Un tableau contenant les colonnes  
            un attribut en_espece de type relation vers espece  
            un attribut en_photo
*   Espèce possède
        un attribut es_photo


Lorsque un document de la famille **Espèce** est mis à jour : pour chaque
document **Enclos** dont **en_espece** référence le document modifié, la valeur
de l’attribut **en_photo** doit être mise à jour avec la valeur de **es_photo**
sur la ligne correspondante

Envoi de la notification

    [php]
    class Zoo_Espece extends Family\Document
    {
        public function postStore()
        {
            $err=parent::postStore();
            if (empty($err) && $this->isChanged()) {
            $e = new \Dcp\DocEventUpdate(\Dcp\DocEventUpdate::docEventUpdateType, $this);
                Events::dispatch($e);
            }
            return $err;
        }
    }

Pose de l'écoute

    [php]
    class Zoo_Enclos_ extends Family\Document
    {
        public function postStore()
        {
            $err = parent::postStore();
            if ($this->isChanged()) {
                // écoute sur l'enclos
               
                 /* Filter :
                    "initid <@ $en_espece",
                    "updated @> es_photo"
                */
                
                $eventFilter = array(
                    sprintf("%s <@ %d", 
                        \Dcp\DocEventUpdate::dataInitid, 
                        $this->getAttributeValue(Attribute\Zoo_enclos::en_espece)),
                    sprintf("%s @> '%s'", 
                         \Dcp\DocEventUpdate::dataUpdateValues, 
                        Attribute\Zoo_espece::es_photo)
                );
                
                
                $edl = new \Dcp\EventDocListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,
                    $this, $eventFilter
                );
                
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->setCallBackMethod("::refreshPhoto()");
                // pose de l'écoute
                Events::addOrUpdateListener($edl );
            }
            return $err;
        }
        public function refreshPhoto(\Dcp\DocEventUpdate $e)
        {
            /** @var \Dcp\Family\Zoo_espece $doc */
            $espece = $e->getDocument();
            $values = $this->getAttributeValue(Attribute\Zoo_enclos::en_t_especes);
            foreach ($values as &$row) {
                if ($row[Attribute\Zoo_enclos::en_espece] == $doc->initid) {
                    $row[Attribute\Zoo_enclos::en_photo] = $espece->getRawValue(Attribute\Zoo_espece::es_photo);
                }
            }
            $doc->setAttributeValue(Attribute\Zoo_enclos::en_t_especes, $values);
            if ($doc->isChanged()) {
                $doc->store();
            }
        }
    }
    
Avec les méthodes au lieu du tableau pour le filtre :

    [php]
    $edl = new \Dcp\EventDocListener(
        \Dcp\DocEventUpdate::docEventUpdateType,
        $this, $eventFilter
    );
    $edl->assertTargetInitidIsIncludedIn($this->getAttributeValue(Attribute\Zoo_enclos::en_espece));
    $edl->assertTargetModifiedAttributeIncludes(Attribute\Zoo_espece::es_photo);
    $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
    $edl->setCallBackMethod("::refreshPhoto()");
    // pose de l'écoute
    Events::addOrUpdateListener($edl );


## Use Case 3 (avancé) :

Soit les familles Animal et Espece.

*   Animal possède
        un attribut an_espece de type relation vers Espece

*   Espece possède
        peu importe


Lorsque un document de la famille **Espece** est mis à jour :

pour chaque document **Animal** dont **an_espece** référence le document
modifié, la méthode **Animal::refreshChilds** doit être lancée.

Elle a accès à :

*   Les caractéristiques de Espece
*   un tableau des valeurs mises à jour
*   la date et heure de mise à jour de Espece


Envoi de la notification

    [php]
    class Zoo_Espece extends Family\Document
    {
        public function postStore()
        {
            $err=parent::postStore();
            if (empty($err) && $this->isChanged()) {
                $e=new \Dcp\DocEventUpdate(\Dcp\DocEvent::update, $this);
                Events::dispatch($e);
            }
            return $err;
        }
    }

Pose de l'écoute :


### Version 1

Comme d'habitude  depuis chaque animaux.
Cela suppose que tous les animaux ont tous leur écoute propre.

    [php]
    class Zoo_Animal extends Family\Document
    {
        public function postStore()
        {
            $err = parent::postStore();
            if ($this->isChanged()) {
                // écoute sur l'enclos
                $edl = new \Dcp\EventDocListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,
                    $this
                );
                 /* Filter :
                    "initid <@ $an_enclos",
                */
                $edl->assertTargetInitidEquals($this->getAttributeValue(Attribute\Zoo_animal::an_enclos));
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->setCallBackMethod("::refreshChilds()");
                // pose de l'écoute
                Events::addOrUpdateListener($edl );
            }
            return $err;
        }
    }
    
### Version 2

De manière globale.

Soit la classe

    [php]
    class EventFamilyListener extends EventListener {
        
        public function setCallBackMethod($code)
        {
        }
        
        public function assertTargetInitidEqualsToAttribute($attrid)
        {
        }
    }

Ajout d'une écoute globale.

    [php]
    $edl = new \Dcp\EventFamilyListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,
                    \Dcp\Family\Zoo_animal::familyName);
                    
                    
    $edl->setCallBackMethod("::refreshChilds()");
    $edl->assertTargetInitidEqualsToAttribute(Attribute\Zoo_animal::an_enclos);
    Events::addListener($edl);
    

### Version 3

Avec un listener basé sur une recherche.
Applicable que sur les animaux avec enfants.

    [php]
    class EventDocumentListListener extends EventFamilyListener {
        public function setDocumentList($attrid)
        {
            
        }
    }


    [php]
    $edl = new \Dcp\EventDocumentListListener(
                \Dcp\DocEventUpdate::docEventUpdateType);
                
    $s=new \SearchDoc("",\Dcp\Family\Zoo_animal::familyName);
    $s->setObjectReturn(true);
    $s->addFilter(sprintf("%s is not null", Attribute\Zoo_animal::an_enfant));
    $edl->setDocumentList($s->getDocumentList());

    $edl->assertTargetInitidEqualsToAttribute(Attribute\Zoo_animal::an_enclos);
    $edl->setCallBackMethod("::refreshChilds()");
    Events::addListener($edl);