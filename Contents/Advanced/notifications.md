# Notifications

## Use Case 1 (standard) :

Soit les familles Animal et Enclos.

*   Animal possède  
        un attribut an_enclos de type relation vers Enclos  
        un attribut an_enclossurface
*   Enclos possède  
        un attribut en_surface


Lorsque un document de la famille **Enclos** est mis à jour : pour chaque
document Animal dont **an_enclos** référence le document modifié, la valeur de
l’attribut **an_enclossurface** doit être mise à jour avec la valeur de **en_surface**


Envoi de la notification

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
                $e=new \Dcp\DocEvent(\Dcp\DocEvent::update, $this);
                Events::dispatch($e);
            }
            return $err;
        }
    }

Pose de l'écoute

    [php]
    $ef=new \Dcp\EventFilter();
    $ef->addFilterCode(\Dcp\DocEvent::update);
    $ef->addFilter("%s.%s = %s",
        Family\Zoo_animal::familyName,
        Attribute\Zoo_animal::an_enclos,
        \Dcp\DocEvent::documentIdentifier);
        
    /// add optional filter to not update already good relation
    $ef->addFilter("%s.%s = %s.%s",
        Family\Zoo_animal::familyName,
        Attribute\Zoo_animal::an_enclossurface,
        \Dcp\DocEvent::documentAttribute,
        Attribute\Zoo_enclos::en_surface);
        
    Events::addListener($ef, function (\Dcp\DocEvent $e) {
        /** @var Family\Zoo_animal $doc  */
       $doc=$e->getDocument();
       $doc->setValue(Attribute\Zoo_animal::an_enclossurface,
                      Attribute\Zoo_enclos::en_surface );
       if ($doc->isChanged()) {
         $doc->store();
       }
    });

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
                $e=new \Dcp\DocEvent(\Dcp\DocEvent::update, $this);
                Events::dispatch($e);
            }
            return $err;
        }
    }

Pose de l'écoute

    [php]
    $ef=new \Dcp\EventFilter();
    $ef->addFilterCode(\Dcp\DocEvent::update);
    
    // filtre un des éléments de en_espèce correspond à l'espèce modifiée
    $ef->addFilter("%s.%s ~ '\\\\y%s\\\\y",
        Family\Zoo_enclos::familyName,
        Attribute\Zoo_enclos::en_espece,
        \Dcp\DocEvent::documentIdentifier);
    Events::addListener($ef, function (\Dcp\DocEvent $e) {
        /** @var Family\Zoo_enclos $doc  */
       $doc=$e->getDocument();
       $values=$doc->getAttributeValue(Attribute\Zoo_enclos::en_t_especes);
        foreach ($values as &$row) {
            if ($row[Attribute\Zoo_enclos::en_espece] == $doc->initid) {
                $row[Attribute\Zoo_enclos::en_photo] = $doc->getRawValue(Attribute\Zoo_espece::es_photo);
            }
        }
       $doc->setAttributeValue(Attribute\Zoo_enclos::en_t_especes,$values);
       if ($doc->isChanged()) {
         $doc->store();
       }
    });

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
                Events::dispatch($e);
            }
            return $err;
        }
    }

Pose de l'écoute :

    [php]
    $ef=new \Dcp\EventFilter();
    $ef->addFilterCode(\Dcp\DocEvent::update);
    
    $ef->addFilter("%s.%s = %s",
        Family\Zoo_animal::familyName,
        Attribute\Zoo_animal::an_espece,
        \Dcp\DocEvent::documentIdentifier);
    Events::addListener($ef, function (\Dcp\DocEvent $e) {
        /** @var Family\Zoo_animal $doc  */
       $doc=$e->getDocument();
       $changedRawValues=$e->getOldRawValues();
        $changedRawValues = $e->getSendDate(); // date à laquelle l'événement a été lancé
        $mdate=date('Y-m-dTh:i:s', $doc->revdate); // date de modification du doc
        $doc->refreshChilds($changedRawValues, $changedRawValues);
    });