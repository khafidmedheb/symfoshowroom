
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

php bin/console server:run

## Créer une entité Nom
======

$ php bin/console make:entity (puis nommer Nom)


## Installer Doctrine-Fixtures
======

$ composer require --dev doctrine/doctrine-fixtures-bundle

...(fichier AppFixtures.php créé dans src/Entity/AppFixtures.php)

php bin/console doctrine:fixtures:load



# Git workflow Gitkraken possible pour votre projet
======

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


# EN CAS D'UN MERGE FAILED (VIA LA CONSOLE)
======

$ git status

$ git rebase --abort

$ git checkout dev

$ git pull

$ git merge features/<ma_branche>

$ git checkout dev

$ git push

...TODO : A compléter...


# CREATION USER ET ADMIN MDP 1234 AVEC FOSUSERBUNDLE
======

php bin/console fos:user:create user user@test.test 1234

php bin/console fos:user:create admin admin@test.test 1234

php bin/console fos:user:promote admin ROLE_ADMIN


# CRÉATION D'UN GRANT USER VIA MYSQL CLIENT
======

mysql -uroot -p (puis entrer votre MDP utilisateur Linux ou autre OS)

GRANT ALL on <nom_base_mysql>.* to <votre_identifiant>@127.0.0.1 identified by '<votre_mot_de_passe>';

# RECONSTITUTION DE LA BDD
======

$ php bin/console doctrine:database:drop --force

$ php bin/console doctrine:database:create

$ php bin/console make:migration

$ php bin/console doctrine:migrations:migrate


# LOADING D'UN JEU DE DATA (FIXTURES)
======

$ php bin/console doctrine:fixtures:load

# CHANGEMENT ENTITE(S) (BASE DE DONNEES)
======

...Modification éventuelle de src/datafixtures/app.fixture en conséquence

$ php bin/console doctrine:fixtures:load

# INSTALLATION CHROMEDRIVER ET SELENIUM
======

$ Java -Dwebdriver.chrome.driver=C:/wamp64/www/seqOIA/vendor/dmore/chrome-mink-driver/src/Chromedriver -jar C:/Users/khafidmedheb/Documents/Khalid/selenium-server-standalone-3.14.0.jar

$ Java -jar C:/Users/khafidmedheb/Documents/Khalid/selenium-server-standalone-3.14.0.jar -Dwebdriver.chrome.driver=C:/wamp64/www/seqOIA/vendor/dmore/chrome-mink-driver/src/Chromedriver 

$ VERSION=$(curl http://chromedriver.storage.googleapis.com/LATEST_RELEASE)

$ wget https://chromedriver.storage.googleapis.com/$VERSION/chromedriver_win32.zip

$ unzip chromedriver_win32.zip

$ mv chromedriver /usr/bin/chromedriver

# Admin : Lancement de Selenium
======

$ vendor/bin/selenium-server-standalone

# Admin : Fermeture du port 4444 de Selenium
======

$ netstat -ano | findstr :4444 -> affiche <your_PID> dans le result

$ tskill <your_PID>

# LANCEMENT DE CHROME
======

## Run Chrome with interface (Windows)
======

$ start chrome --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222

# headless mode (Windows)
======

$ start chrome --disable-gpu --headless --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222

#  headless mode (Linux) -> ma distrib Ubuntu perso
======

$ google-chrome-stable --no-sandbox --headless --disable-gpu --remote-debugging-port=9222 http://127.0.0.1:8000

# Problème d'allocation mémoire quand on utilise composer
======

$ php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar update


# Base documentaire :
======

## Rédiger en markdown : https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
