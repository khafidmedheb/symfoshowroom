# symfoshowroom
Application "Ecole" pour apprendre à utiliser Symfony 4 par l'exemple.


                                           #### COMMANDES USUELLES ####


#### CREATION USER ET ADMIN MDP 1234 AVEC FOSUSERBUNDLE ####
php bin/console fos:user:create user user@test.test 1234

php bin/console fos:user:create admin admin@test.test 1234
php bin/console fos:user:promote admin ROLE_ADMIN


#### GIT WORKFLOW DE SEQOIA - CHECKLIST ####
#### COMMIT/PUSH DE MES DEVS SUR FEATURE/<MA_BRANCHE> ####
Je suis sur <ma_branche>

Fin des dev

0) Cleaner le code avec la commande suivante (à lancer une 2ème fois si F apparaît dans le résultat) :

  $ ./vendor/bin/php-cs-fixer fix --using-cache=no --verbose --diff --rules=@Symfony src 

  Remarque : Après le php-cs-fixer, vous risquez de voir des fichiers sur lesquels vous n'avez pas travaillé, dans 
  la zone "stage" (avant git add -A) 

1) Stage "all changes" > Titre du commit > Commit

2) Pull
Remarque "flèches" : 
  Si flèche vers le bas sur <ma_branche> -> faire un pull
  Si flèche vers le haut sur <ma_branche> -> faire un push

3) push vers <ma_branche> (je suis sur <ma_branche>)

4) Checkout "dev"

5) Pull (de la dev distante vers ma dev en local)

6) Checkout <ma_branche>

7) Clique droit sur <dev> > "Rebase <ma_branche> onto dev"

     Attention : après l'étape 7), 2 flèches "haut" et "bas" apparaissent à côté de <ma_branche>

     7 bis) Pull (note : pull de <ma_branche> qui a la flèche vers le bas)

     7 ter) Push (note : push de <ma_branche> qui a la flèche vers le haut)

     Si erreur sur le rebase : cliquer en haut du diagramme central sur "Work in progress" (WP) puis sur "skip commit" 
     (en bas à droite)

10) Clique droit <dev> > Merge <ma_branche> into dev

11) Checkout "dev"

12) Push

13) Ne pas oublier : Checkout <ma_branche> avant les prochains développements


#### EN CAS D'UN MERGE FAILED (VIA LA CONSOLE) ####
$ git status
$ git rebase --abort
$ git checkout dev
$ git pull
$ git merge features/tests_behat
$ git checkout dev
$ git push

#### RECONSTITUTION DE LA BDD ####
$ php bin/console doctrine:database:drop --force
$ php bin/console doctrine:database:create
$ php bin/console make:migration
$ php bin/console doctrine:migrations:migrate

#### LOADING D'UN JEU DE DATA (FIXTURES) ####
$ php bin/console doctrine:fixtures:load

#### CHANGEMENT ENTITE(S) (BASE DE DONNEES) ####
Modification éventuelle de src/datafixtures/app.fixture en conséquence

$ php bin/console doctrine:fixtures:load

#### INSTALLATION CHROMEDRIVER ET SELENIUM ####
Java -Dwebdriver.chrome.driver=C:/wamp64/www/seqOIA/vendor/dmore/chrome-mink-driver/src/Chromedriver -jar C:/Users/khafidmedheb/Documents/Khalid/selenium-server-standalone-3.14.0.jar
Java -jar C:/Users/khafidmedheb/Documents/Khalid/selenium-server-standalone-3.14.0.jar -Dwebdriver.chrome.driver=C:/wamp64/www/seqOIA/vendor/dmore/chrome-mink-driver/src/Chromedriver 

# Admin : Lancement de Selenium
vendor/bin/selenium-server-standalone

# Admin : Fermeture du port 4444 de Selenium
- netstat -ano | findstr :4444 -> affiche <your_PID> dans le result
- tskill <your_PID>

VERSION=$(curl http://chromedriver.storage.googleapis.com/LATEST_RELEASE)
wget https://chromedriver.storage.googleapis.com/$VERSION/chromedriver_win32.zip
unzip chromedriver_win32.zip
mv chromedriver /usr/bin/chromedriver

#### LANCEMENT DE CHROME ####
# Run Chrome with interface (Windows)
start chrome --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222

# headless mode (Windows)
start chrome --disable-gpu --headless --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222

#  headless mode (Linux)
chrome --disable-gpu --headless --remote-debugging-address=0.0.0.0 --remote-debugging-port=9222

# Problème d'allocation mémoire quand on utilise composer
# erreur du type : 

php -dmemory_limit=-1 C:/ProgramData/ComposerSetup/bin/composer.phar update
