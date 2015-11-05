# Définir un workflow par programmation

Introduction de nouvelles classes d'objets afin de spécifier le workflow. Ceci
permet de ne plus avoir tableau déclaratif et de ne manipuler que des objets aux
caractéristiques définies par rapport à de simples tableaux indexés.

## Nouvelles classes d'objet de workflow
Classe de transition

    [php]
    class WTransition
    {
        public $id;
        public function __construct(WStep $e1, WStep $e2, WTransitionType $t)
        {
        }
       
    }

Classe d'étape :

    [php]
    class WStep
    {
        public $id;
        public function __construct($id, $stateLabel = '', $activityLabel = '')
        {
        }
        /**
         * @return WStep
         */
        public function isFirstState($isFirst=true)
        {
        return $this;
        }
        /**
         * @return WStep
         */
        public function getStateLabel()
        {
        }
        /**
         * @return WStep
         */
        public function getActivityLabel()
        {
        return $this;
        }
        /**
         * @return WStep
         */
        public function setStateLabel()
        {
        return $this;
        }
        /**
         * @return WStep
         */
        public function setActivityLabel()
        {
        return $this;
        }
    }

Classe de type de transition :

    [php]
    class WTransitionType
    {
        public $id;
        public function __construct($id)
        {
        }
        /**
         * @param callable $call
         * @return WTransitionType
         */
        public function setLabel($call)
        {
        return $this;
        }
        /**
         * @param callable $call
         * @param string  $label
         * @return WTransitionType
         */
        public function setM0($call, $label)
        {
        return $this;
        }
        /**
         * @param callable $call
         * @param string  $label
         * @return WTransitionType
         */
        public function setM1($call, $label)
        {
        return $this;
        }
        /**
         * @param callable $call
         * @param string  $label
         * @return WTransitionType
         */
        public function setM2($call, $label)
        {
        return $this;
        }
        /**
         * @param callable $call
         * @param string  $label
         * @return WTransitionType
         */
        public function setM3($call, $label)
        {
        return $this;
        }
        /**
         * @param array $asks
         * @return WTransitionType
         */
        public function setAsk(array $asks)
        {
        return $this;
        }
        /**
         * @param bool $noReason
         * @return WTransitionType
         */
        public function setNoReason($noReason=true)
        {
        return $this;
        }
    }


## Utilisation des classes

    [php]
    use  \Dcp\AttributeIdentifiers\Wbasictest as AWObject;
    use  \Dcp\AttributeIdentifiers\Basictest as ABasic;
    /**
     * Class WObject
     * @method addStep(Wstep $e1)
     * @method addTransitionType( WTransitionType $t)
     * @method addTransition (Wstep $e1, WStep $e2, WTransitionType $t)
     */
    class WObject extends \Dcp\Family\WDoc
    {
        public $attrPrefix = "WDT";
      // state names
        const initialised = "wdt_initialised";
        const transmited = "wdt_transmited";
        const accepted = "wdt_accepted";
        const refused = "wdt_refused";
        const published = "wdt_published";
        
        // transition names
        const Ttransmition = "wdt_transmition";
        const Taccept = "wdt_accept";
        const Trefused = "wdt_refuse";
        const Tretry = "wdt_retry";
        const Trealise = "wdt_realise";
        
        public function initialize()
        {
            $stepInitialized = new WStep(self::initialised,
                        _("zoo:state:initialised"),
                        _("zoo:activity:initialised"));
            $stepInitialized->isFirstState();
            $this->addStep($stepInitialized);
            $stepTransmited = new WStep(self::transmited);
            $stepTransmited->setActivityLabel(_("zoo:state:transmited"))->setStateLabel(_("zoo:state:transmited"));
            
            $this->addStep($stepTransmited);
            $stepAccepted = new WStep(self::transmited,
                        _("zoo:state:accepted"),
                        _("zoo:activity:accepted"));
            $this->addStep($stepAccepted);
            
            $stepRefused = new WStep(self::refused,
                        _("zoo:state:refused"));
            $this->addStep($stepRefused);
            $stepPublished = new WStep(self::published,
                        _("zoo:state:published"));
            $this->addStep($stepPublished);
            
            $transitionTransmition=new WTransitionType(self::Ttransmition);
            $transitionTransmition->setLabel(_("zoo:trans:transmition"));
            $transitionTransmition->setM0(function($newStep, $currentStep) {
                $this->myFirstCondition($newStep, $currentStep);}, _("My pre-cond")
            );
            $transitionTransmition->setM1(function($newStep, $currentStep, $comment) {
                $this->mySecondCondtion($newStep, $currentStep, $comment);}, _("My cond")
            );
            $transitionTransmition->setM2(function($currentStep, $previousStep) {
                $this->myFirstProcess($currentStep, $previousStep);}, _("Post Process")
            );
            $transitionTransmition->setM3(function($currentStep, $previousStep) {
                $this->myLastProcess($currentStep, $previousStep);}, _("Last Process")
            );
            $this->addTransitionType($transitionTransmition);
            
            
            $transitionTaccept=new WTransitionType(self::Taccept);
            $transitionTransmition->setLabel(_("zoo:trans:accept"));
            $transitionTaccept->setAsk(array(AWObject::wdf_levelmax1));
            $transitionTaccept->setNoReason(true);
            $this->addTransitionType($transitionTaccept);
            
            $transitionTrefused=new WTransitionType(self::Trefused);
            $transitionTransmition->setLabel(_("zoo:trans:refused"));
            $transitionTrefused->setM1(function($newStep, $currentStep, $comment) {
                $this->myGlobalTest($newStep, $currentStep, $comment);}, _("My global test")
            );
            $transitionTrefused->setAsk(array(AWObject::wdf_globalmax1, AWObject::wdf_globalmax2));
            $transitionTrefused->setNoReason(true);
            $this->addTransitionType($transitionTrefused);
            
            $transitionTrealise=new WTransitionType(self::Trealise);
            $transitionTransmition->setLabel(_("zoo:trans:realise"));
            $this->addTransitionType($transitionTrealise);
            
            $transitionTretry=new WTransitionType(self::Tretry);
            $transitionTransmition->setLabel(_("zoo:trans:retry"));
            $transitionTretry->setNoReason(true);
            $this->addTransitionType($transitionTretry);
            
            $this->addTransition($stepInitialized, $stepTransmited, $transitionTransmition);
            $this->addTransition($stepTransmited, $stepAccepted, $transitionTaccept);
            $this->addTransition($stepTransmited, $stepRefused, $transitionTrefused);
            $this->addTransition($stepAccepted, $stepPublished, $transitionTrealise);
            $this->addTransition($stepTransmited, $stepRefused, $transitionTretry);
        }
        /**
         * @param string $newStep next step id
         * @param string $currentStep current step id
         * @return string error message
         */
        public function myGlobalTest($newStep, $currentStep)
        {
            $err = '';
            $level1 = $this->getInstanceValue(ABasic::bat_level1);
            $param1 = $this->getRawValue(AWObject::wdf_globalmax1); // here get transition paramter
            $param2 = $this->getRawValue(AWObject::wdf_globalmax2); // here get transition paramter
            if ($level1 > $param1 || $level1 > $param2) {
                $err = sprintf("Level one [%d] must be lesser then  [%d]", $level1, min($param1, $param2));
            }
            return $err;
        }
        
        /**
         * @param string $newStep next step id
         * @param string $currentStep current step id
         * @return string error message
         */
        public function myFirstCondition($newStep, $currentStep)
        {
            $err = '';
            $level1 = $this->getInstanceValue(ABasic::bat_level1);
            $level2 = $this->getInstanceValue(ABasic::bat_level2);
            if ($level1 < $level2) {
                $err = sprintf("Level one [%d] must be greater than level two [%d]", $level1, $level2);
            }
            return $err;
        }
        
        /**
         * @param string $newStep next step id
         * @param string $currentStep current step id
         * @return string error message
         */
        public function myLevelCondition($newStep, $currentStep)
        {
            $err = '';
            $level1 = $this->getInstanceValue(ABasic::bat_level1);
            $max1 = $this->getRawValue(AWObject::wdf_levelmax1);
            if ($level1 > $max1) {
                $err = sprintf("Level one [%d] must be lesser than max [%d]", $level1, $max1);
            }
            return $err;
        }
        
        /**
         * @param string $currentStep current step id
         * @param string $previousStep previous step id
         * @return string  message
         */
        public function myFirstProcess($currentStep, $previousStep)
        {
            $level2 = $this->getInstanceValue(ABasic::bat_level2);
            $err = $this->doc->setValue(ABasic::bat_level2, $level2 + 1);
            if (!$err) $err = $this->doc->store();
            return $err;
        }
        
        /**
         * @param string $currentStep current step id
         * @param string $previousStep previous step id
         * @return string  message
         */
        public function myLastProcess($currentStep, $previousStep)
        {
            $err = '';
            $level1 = $this->getInstanceValue(ABasic::bat_level1);
            $level2 = $this->getInstanceValue(ABasic::bat_level2);
            $this->doc->addHistoryEntry(sprintf("Difference level is %d", $level1 - $level2));
            return $err;
        }
        
        /**
         * @param string $newStep next step id
         * @param string $currentStep current step id
         * @param string $comment transition comment
         * @return string error message
         */
        public function mySecondCondtion($newStep, $currentStep, $comment)
        {
            $err = '';
            $level1 = $this->getInstanceValue(ABasic::bat_level1);
            $level2 = $this->getInstanceValue(ABasic::bat_level2);
            if ($level1 < $level2) {
                $err = sprintf("Level one [%d] must be greater than level two [%d]", $level1, $level2);
            }
            return $err;
        }
        public function getFirstState()
        {
            $u = getCurrentUser();
            $userRole = $u->getAllRoles();
            // test if current user has bigboss role
            foreach ($userRole as $roleProps) {
                if ($roleProps["login"] == "bigboss") {
                    return self::accepted;
                }
            }
            return $this->firstState;
        }
    }
