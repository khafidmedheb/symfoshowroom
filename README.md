
# MON FICHIER ADMIN - COMMANDES USUELLES
------

# Set-up de mon environnement Symfony 4
======

$ composer create-project symfony/skeleton <nom_projet>

$ cd <nom_projet>

$ composer require symfony/orm-pack

$ composer require annotations

$ composer require validator

$ composer require template

$ composer require security-bundle

$ composer require --dev maker-bundle

## Créer un controller NomController
======

$ php bin/console make:controller (puis nommer NomController -> en CamelCase)

$ composer require server --dev


## Lancer le serveur Symfony
======

$ php bin/console server:run

Pour Mercury :

$ php bin/console server:run --env=dev --docroot=web/

(Puis aller sur  http://127.0.0.1:8000 pour votre projet sur le browser comme indiqué)

## Créer une entité Nom
======

$ php bin/console make:entity (puis nommer Nom)


# Git workflow Gitkraken possible pour votre projet
======

  Accéder à mon compte Github :

    Username for 'https://github.com': khafidmedheb
    Password:xxxxxxx

## Cleaner le code pour le rendre à la norme PSR 

...(à lancer une 2ème fois si F apparaît dans le résultat) :

$ ./vendor/bin/php-cs-fixer fix --using-cache=no --verbose --diff --rules=@Symfony src  

...Remarque : Après le php-cs-fixer, vous risquez de voir des fichiers sur lesquels vous n'avez pas travaillé, dans 
la zone "stage" (avant git add -A) 

1. Stage "all changes" > Titre du commit > Commit

2. Pull

...Remarque "flèches" : 
...Si flèche vers le bas sur <ma_branche> -> faire un pull
...Si flèche vers le haut sur <ma_branche> -> faire un push

3. push vers <ma_branche> (je suis sur <ma_branche>)

4. Checkout "dev"

5. Pull (de la dev distante vers ma dev en local)

6. Checkout <ma_branche>

7. Clique droit sur <dev> > "Rebase <ma_branche> onto dev"

...Attention : après l'étape 7), 2 flèches "haut" et "bas" apparaissent à côté de <ma_branche>

7bis. Pull (note : pull de <ma_branche> qui a la flèche vers le bas)

7ter. Push (note : push de <ma_branche> qui a la flèche vers le haut)

...Si erreur sur le rebase : cliquer en haut du diagramme central sur "Work in progress" (WP) puis sur "skip commit" 
(en bas à droite)

10. Clique droit <dev> > Merge <ma_branche> into dev

11. Checkout "dev"

12. Push

13. Ne pas oublier : Checkout <ma_branche> avant les prochains développements


# J'ai fait des modifs sur la branche dev au lieu de ma branche de travail (ex : tests_behat).
# Je souhaite mettre le(s) fichier(s) en attente sur ma branche de travail

1. Je suis sur dev, clique "stash" (bannette virtuelle)
2. Checkout <ma_branche>
3. Rebase <ma_branche> onto dev
4. pull et push éventuels sur <ma_branche>
5. Clique sur "pop" -> le(s) fichier(s) changé(s) en dev sont remis  en attente sur <ma_branche>



## TODO : Commandes Git de base
======

$ git status

$ git rebase --abort

$ git checkout dev

$ git pull

$ git merge features/<ma_branche>

$ git checkout dev

$ git push

...TODO : A compléter...


# Erreur git du type "git pull fails “unable to resolve reference” “unable to update local ref” "
======

ma_branche = feature/test_behat_sf4

$ rm .git/refs/remotes/origin/feature/test_behat_sf4

$ git branch --set-upstream-to=origin/feature/test_behat_sf4

$ git pull

$ git mergetool

$ git commit -m "Correction"

$ git push





# CREATION USER ET ADMIN MDP 1234 AVEC FOSUSERBUNDLE
======

php bin/console fos:user:create user user@test.test 1234

php bin/console fos:user:create admin admin@test.test 1234

php bin/console fos:user:promote admin ROLE_ADMIN

## Installer Doctrine-Fixtures (pour la création d'un jeu de données -> voir # Chargement de données ... )
======

$ composer require --dev doctrine/doctrine-fixtures-bundle

...(fichier AppFixtures.php créé dans src/Entity/AppFixtures.php)

# Dans PhpMyadmin : 
======

Renseigner "a:1:{i:0;s:16:"ROLE_SUPER_ADMIN";}" dans le champ "roles" 


# CRÉATION D'UN GRANT USER VIA MYSQL CLIENT
======

mysql -uroot -p (puis entrer votre MDP utilisateur Linux ou autre OS)

GRANT ALL on <nom_base_mysql>.* to <votre_identifiant>@127.0.0.1 identified by '<votre_mot_de_passe>';

# RECONSTITUTION DE LA BDD
======

-> Supprimer les fichiers "Migrations-xxxxx" du dossier src/migrations

-> Vider la table Migrations de notre bases via PhpMyadmin (sauf si on drop la base entière !)

$ php bin/console doctrine:database:drop --force

$ php bin/console doctrine:database:create

$ php bin/console make:migration

-> Ouvrir le fichier src/Migrations/Versionxxxx.php
-> Ajouter "$this->addSql('ALTER TABLE type_protocol AUTO_INCREMENT=0');" à la fin de up(Schema...)

$ php bin/console doctrine:migrations:migrate


# MISE A JOUR DE LA BDD
======

$ php bin/console doctrine:schema:update --force

$ php bin/console doctrine:schema:validate



# Chargement de données (jeu d'essai ou fixtures)
======

  # By default the load command purges the database, removing all data from every table.

  $ php bin/console doctrine:fixtures:load

  # To append your fixtures' data add the --append option.
  $ php bin/console doctrine:fixtures:load --append

# Chargement de données "réalistes" avec le bundle Faker
======

Possibilité d'utiliser aussi le package Faker de Symfony

-> On peut aussi utiliser le bundle Faker pour avoir des données plus réalistes (nom, adresses, textes lorem,...)
Lien : https://github.com/fzaninotto/Faker





# CHANGEMENT ENTITE(S) (BASE DE DONNEES)
======

...Modification éventuelle de src/datafixtures/app.fixture en conséquence

  $ php bin/console doctrine:fixtures:load

# Nettoyage du cache
======

  $ php bin/console cache:clear

Si erreur mémoire du type : "Error: Allowed memory size of 134217728 bytes exhausted (tried to allocate 131072 bytes)
"
Alors lancer la commande suivante :

  $ php -d memory_limit=-1 bin/console cache:clear

# Installation de Chromedriver, Selenium et Chrome driver
======

    # Windows : Avec le chromedriver.exe (qu'il faut lancer en cliquant sur le fichier -> voir commande suivante)
    ======


    Pour Seqoia :

    $ java -Dwebdriver.chrome.driver=C:/wamp64/www/seqOIA/var/Selenium/chromedriver -jar C:/wamp64/www/seqOIA/var/Selenium/selenium-server-standalone-3.141.59.jar -debug
    
    Pour Ice :

     $ java -Dwebdriver.chrome.driver=C:/wamp64/www/ice/var/Selenium/chromedriver -jar C:/wamp64/www/ice/var/Selenium/selenium-server-standalone-3.141.59.jar -debug

     $ java -Dwebdriver.chrome.driver=C:/wamp64/www/ice/chromedriver -jar C:/wamp64/www/ice/var/Selenium/selenium-server-standalone-3.141.59.jar -debug

      -> On doit voir un serveur (prompt |) en attente avec "INFO - Selenium Server is up and running on port 4444"

    Configuration:
      $ java -jar C:/wamp64/www/ice/var/Selenium/selenium-server-standalone-3.141.59.jar -role hub -hubConfig C:/wamp64/www/ice/var/Selenium/hub-conf.json
      $ java -jar C:/wamp64/www/ice/var/Selenium/selenium-server-standalone-3.141.59.jar -role node -nodeConfig C:/wamp64/www/ice/var/Selenium/win-node-conf.json
    
      $ System.setProperty('Dwebdriver.chrome.driver', 'C:/wamp64/www/ice/var/Selenium/chromedriver');

    Puis aller dans C:/wamp64/www/seqOIA/var/Selenium/ et double cliquer sur le fichier chromedriver.exe
    Une console Msdos devrait s'ouvrir avec l'invite "Starting ChromeDriver ..."

    # Linux (Ubuntu Xenial) 
    ======

# Lancement de Chrome
======

    # (Windows): Run Chrome sans interface (ou headless mode) 
    ======

    $ start chrome --disable-gpu -enable-logging --v=0 --headless --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222
                                                        
    $ start chrome --disable-gpu --headless --no-sandbox --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222 --user-data-dir=/data



    start chrome --disable-gpu -enable-logging --headless --dump-dom http://127.0.0.1:8000
    ## (Windows): Run Chrome with interface 
    ======

    $ start chrome --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222


    # (Linux): Run Chrome sans interface (ou headless mode) -> ma distrib Ubuntu Xenial sur Travis
    ======

    $ google-chrome-stable --no-sandbox --headless --disable-gpu --/prefetch:1 --remote-debugging-port=9222 http://127.0.0.1:8000

    
# Admin : Fermeture du port 4444 de Selenium
======

$ netstat -ano | findstr :4444 -> affiche <your_PID> dans le result

$ tskill <your_PID>



# Problème d'allocation mémoire quand on utilise composer
======
erreur du type : "Fatal error: Allowed memory size of 1610612736 bytes exhausted (tried to allocate 
12288 bytes) in phar://C:/ProgramData/ComposerSetup/bin/composer.phar/src/Composer/
DependencyResolver/GenericRule.php on line 36"  php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require google/apiclient


  # Pour checker composer.json
  $ php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar validate


  # Maj composer.json
  $ php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar update

  # Installation des packages
  $ php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar install

  $ php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require <NOM_PACKAGE>


  $ php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require lovers-of-behat/table-extension

php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require --dev doctrine/doctrine-fixtures-bundle


# Maintenance Travis :
======

# Optimisation builds Travis :
======

## Stages "Travis" : https://medium.com/ubc-launch-pad-software-engineering-blog/optimizing-travis-ci-pipelines-36973aea3758


## Installation Behat

$ php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require --dev behat/behat
$ php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require --dev fabpot/goutte

$ php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require behat/mink --dev


vendor/bin/behat --list-scenarios | ./vendor/liuggio/fastest/fastest "vendor/bin/behat {}"
vendor/bin/behat --list-scenarios | ./vendor/liuggio/fastest/fastest "test-behat.sh {}"

# Requêtes SQL (maintenance) :
======

1) Ajouter 5 ans à une date de péremption

UPDATE consommables SET date_peremption = date_peremption + interval '5' year WHERE id = 1;

remove symfony/symfony v3.0.9

vendor/bin/phpmd src text cleancode, codesize, controversial, design, unusedcode

- vendor/bin/phpcpd src



# Base documentaire :
======

## Rédiger en markdown : https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

Tests stages (share du cache entre 2 stages)

php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require <NOM_PACKAGE>

php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar update rstgroup/behat-oauth2-context


php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar global require behat/behat


## Ne pas afficher les plateformes [win32], [linux32], [mac64], etc....

Dans le fichier composer.json, ajouter dans "extra":
  "lbaey/chromedriver": { "bypass-select": true, "chromedriver-version": "2.35" },"
comme suit

"extra": {
        "lbaey/chromedriver": { "bypass-select": true, "chromedriver-version": "2.35" },




"guzzlehttp/guzzle": "~6.0",
        ...


php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require symfony/console

## Chemin dossier suivi de formation
\\192.168.29.3\evry\09-SMQ\3-Ressources-Humaines\Formations

## Doc action de formation
file://192.168.29.3/evry/09-SMQ/3-Ressources-Humaines/Enregistrements/SMQ-ENR-022-R00%20Evaluation%20d'une%20action%20de%20formation.pdf

php -d memory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar require --dev ingenerator/behat-tableassert

                                                                                             whereis -u -M -f *


                                                                                             xterm -e 'cd /c/wamp64/www/ice && /bin/bash'
