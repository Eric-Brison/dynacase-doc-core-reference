# Accès anonyme (invité) {#core-ref:932e2070-6929-11e2-8218-0021e9fffec1}

L'accès anonyme permet d'accéder à des actions dynacase sans être authentifié.
Les accès sont alors automatiquement fait sous l'identité de l'utilisateur
`anonymous`.

Les applications et actions accessibles en mode anonyme sont alors gérées par
les accessibilités de l'utilisateur `anonymous`.

Accès anonyme par `guest.php`
:   L'accès anonyme effectué par `guest.php`, lance les actions demandés sous
    l'identité de l'utilisateur `anonymous`.

    Cet accès anonyme peut être désactivé en indiquant `no` dans le paramètre
    applicatif  `CORE_ALLOW_GUEST` de l'application _CORE_.
    
    Exemple :
    
        /guest.php?app=FOO&action=BAR

Accès anonyme par `index.php `et `useIndexAsGuest`
:   Le mode anonyme est aussi accessible via le point d'entré standard
    `index.php` lorsque le paramètre `$useIndexAsGuest` est positionné à la
    valeur `true` dans le fichier `config/local-dbaccess.php` :
    
        [php]
        <?php
        
        $useIndexAsGuest = true;
    
    Dans ce mode de fonctionnement, si l'utilisateur `anonymous` a le droit
    d'exécuter l'action demandée, alors l'accès est autorisé et fait sous
    l'identitée du compte `anonymous`.
    
    Par contre, si l'action demandée n'est pas accessible par l'utilisateur
    `anonymous`, alors l'authentification est automatiquement demandée afin que
    l'utilisateur ouvre une session authentifiée pour pouvoir exécuter cette
    action.
    
    C'est donc un mode mixte, et automatique, qui donne l'accès par défaut en
    tant que `anonymous` (comme `guest.php`), mais qui bascule en mode
    authentifié lorsque les droits de `anonymous` ne sont pas suffisants pour
    exécuter l'action demandée.
    
    Pour ouvrir explicitement une session de consultation authentifiée, il faut
    accéder à l'URL de l'application d'authentification spécifique de
    l'Authenticator utilisé. Par exemple pour l'Authenticator `html` :
    `authent.php?app=AUTHENT&action=LOGINFORM`
