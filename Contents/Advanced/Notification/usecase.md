# Étude de cas

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


L'objet `DocEvent` s'occupe de
récupérer les données pour l'utilisation.





Son utilisation dans l'enclos

    [php]
    namespace Zoo;
    use \Dcp\AttributeIdentifiers\MyFamily as Aself;
    use \Dcp\AttributeIdentifiers\Iuser as Aiuser;
    use Dcp\AttributeIdentifiers as Attribute;
    use Dcp\EventManager;
    use Dcp\Family as Family;
    
    class Zoo_Enclos extends Family\Document
    {
        public function postStore()
        {
            $err=parent::postStore();
            if (empty($err) && $this->isChanged()) {
                $e = new \Dcp\DocEvent(\Dcp\DocEvent::docEventUpdateType, $this);
                EventManager::dispatch($e);
            }
            return $err;
        }
    }

### pose de l'écoute 


    [php]
    class Zoo_Animal extends Family\Document
    {
        public function postStore()
        {
            $err = parent::postStore();
            if ($this->isChanged()) {
                // écoute sur l'enclos
               
                
                $edl = new \Dcp\EventDocListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,// filtre sur le type de l'événement
                    $this, $eventFilter
                );
                $edl->assertTargetInitidEquals($this->getAttributeValue(Attribute\Zoo_animal::an_enclos));
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->setCallBackMethod("::refreshEnclos()");
                // pose de l'écoute
                \Dcp\DocEventManager::addOrUpdateListener($edl );
            }
            return $err;
        }
        
        public function refreshEnclos(\Dcp\DocEvent $e)
        {
            $enclos = $e->getTargetDocument();
            $this->setValue(Attribute\Zoo_animal::an_enclossurface,
                $enclos->getRawValue(Attribute\Zoo_enclos::en_surface));
            if ($this->isChanged()) {
                $this->store();
            }
        }
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
                EventManager::dispatch($e);
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
               
                
                
                $edl = new \Dcp\EventDocListener(
                    \Dcp\DocEventUpdate::docEventUpdateType,
                    $this, $eventFilter
                );
                
    
                $edl->assertTargetInitidIsIncludedIn($this->getAttributeValue(Attribute\Zoo_enclos::en_espece));
                $edl->assertTargetModifiedAttributeIncludes(Attribute\Zoo_espece::es_photo);
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->assertTargetFromNameMatch("ZOO_ESPECE");
                $edl->setCallBackMethod("::refreshPhoto()");
                // pose de l'écoute
                EventManager::addOrUpdateListener($edl );
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
                $e=new \Dcp\DocEvent(\Dcp\DocEvent::update, $this);
                EventManager::dispatch($e);
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
                    "initid = $an_enclos",
                */
                $edl->assertTargetInitidEquals($this->getAttributeValue(Attribute\Zoo_animal::an_enclos));
                $edl->setUniqueId(sprintf("listen-poststore-%d", $this->initid));
                $edl->setCallBackMethod("::refreshChilds()");
                // pose de l'écoute
                EventManager::addOrUpdateListener($edl );
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
    $edl = new \Dcp\FamilyEventListener(
                    \Dcp\DocEvent::docEventUpdateType,
                    \Dcp\Family\Zoo_animal::familyName);
                    
                    
    $edl->setCallBackMethod("::refreshChilds()");
    $edl->assertTargetInitidEqualsToAttribute(Attribute\Zoo_animal::an_enclos);
    EventManager::addListener($edl);
    

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
    EventManager::addListener($edl);