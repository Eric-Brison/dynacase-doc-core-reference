# La famille de Workflow (version 2)

Ajout méthode hook `initialize`.  Cette méthode est appelée par le constructeur
de workflow lors de son initialisation.

Ce contenu pourrait aussi être mis dans la méthode native `__construct`, mais il
est préférable d'isoler explicitement la méthode de construction du cycle.


Ajout de l'attribut `$step` qui permet de décrire l'ensemble des étapes.

    [php]
    class WNewLabel extends WDoc
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
        public $firstState = self::initialised;
        
        public $steps = array(); /* nouvel attribut */
        
        public function initialize()
        {
            $this->steps = array(
                self::initialised => array(
                    "stateLabel" => _("zoo:state:initialised"),
                    "activityLabel" => _("zoo:activity:initialised")
                ),
                self::transmited => array(
                    "stateLabel" => _("zoo:state:transmited"),
                    "activityLabel" => _("zoo:activity:transmited")
                ),
                self::accepted => array(
                    "stateLabel" => _("zoo:state:transmited"),
                    "activityLabel" => _("zoo:activity:transmited")
                ),
                self::refused => array(
                    "stateLabel" => _("zoo:state:refused"),
                    "activityLabel" => ""
                ),
                self::published => array(
                    "stateLabel" => _("zoo:state:published"),
                    "activityLabel" => ""
                )
            );
        }
        // transition type
        public $transitions = array(
            self::Ttransmition => array("m0" => "myFirstCondition",
                "m1" => "mySecondCondtion",
                "m2" => "myFirstProcess",
                "m3" => "myLastProcess"
            ),
            self::Taccept => array(
                "ask" => array("wdf_levelmax1"),
                "nr" => true),
            self::Trefused => array(
                "m1" => "myGlobalTest",
                "ask" => array("wdf_globalmax1", "wdf_globalmax2"),
                "nr" => true),
            self::Trealise => array(),
            self::Tretry => array("nr" => true)
        );
        public $cycle = array(
             array(
                 "e1" => self::initialised,
                 "e2" => self::transmited,
                 "t" => self::Ttransmition
             ),
             array(
                 "e1" => self::transmited,
                 "e2" => self::accepted,
                 "t" => self::Taccept
             ),
             array(
                 "e1" => self::transmited,
                 "e2" => self::refused,
                 "t" => self::Trefused
             ),
             array(
                 "e1" => self::accepted,
                 "e2" => self::published,
                 "t" => self::Trealise
             ),
             array(
                 "e1" => self::transmited,
                 "e2" => self::initialised,
                 "t" => self::Tretry
             )
         );
         
        /**
         * @param string $newStep next step id
         * @param string $currentStep current step id
         * @return string error message
         */
        public function myGlobalTest($newStep, $currentStep)
        {
            $err = '';
            $level1 = $this->getInstanceValue("bat_level1");
            $param1 = $this->getRawValue("wdf_globalmax1"); // here get transition paramter
            $param2 = $this->getRawValue("wdf_globalmax2"); // here get transition paramter
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
            $level1 = $this->getInstanceValue("bat_level1");
            $level2 = $this->getInstanceValue("bat_level2");
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
            $level1 = $this->getInstanceValue("bat_level1");
            $max1 = $this->getRawValue("wdf_levelmax1");
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
            $level2 = $this->getInstanceValue("bat_level2");
            $err = $this->doc->setValue("bat_level2", $level2 + 1);
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
            $level1 = $this->getInstanceValue("bat_level1");
            $level2 = $this->getInstanceValue("bat_level2");
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
            $level1 = $this->getInstanceValue("bat_level1");
            $level2 = $this->getInstanceValue("bat_level2");
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