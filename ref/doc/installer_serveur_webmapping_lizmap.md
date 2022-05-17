Louis Manière
Date : 14/04/2022
--------------------------------

Description : 
installation en local avec ubuntu 20.04 d'un serveur de partage de carte intéractive Lizmap
ici Lizmap 3.5.0 avec qgis-server 3.22.5 apache2 et php7.3
installation d'Apache2
installation de QGIS serveur
installation de Lizmap
diffusion d'une carte lizmap depuis QGIS

--------------------------------

Ressources :

# Procédure générale :
https://georezo.net/forum/viewtopic.php?id=118349
https://github.com/3liz/lizmap-web-client/issues/1388
# Installation de Lizmap
https://docs.lizmap.com/current/fr/install/linux.html
# choix de la version de PHP
https://devanswers.co/install-apache-mysql-php-lamp-stack-ubuntu-20-04/
# documentation QGSI server
https://docs.qgis.org/3.22/en/docs/server_manual/index.html
# github lizmap web client - voir INSTALL.md surtout pour les versions
https://github.com/3liz/lizmap-web-client

--------------------------------

Dans un terminal

1- installation d'apache2, PHP et QGIS-server

sudo apt-get update
sudo apt install apache2

# vérifier l'installation d'apache2
http://localhost:80

# attention de vérifier la verios actuelle de php avec celle d'apache2
# voir https://devanswers.co/install-apache-mysql-php-lamp-stack-ubuntu-20-04/
sudo apt-get install php7.3-fpm php7.3-cli php7.3-bz2 php7.3-curl php7.3-gd php7.3-intl php7.3-json php7.3-mbstring php7.3-pgsql php7.3-sqlite3 php7.3-xml php7.3-ldap

# attention aux choix de version à installer, LTR ou non
# compatibilité avec la version du client lizmap : https://github.com/3liz/lizmap-web-client/wiki/Versions
sudo apt install qgis-server libapache2-mod-fcgid
sudo a2enmod fcgid
sudo a2enconf serve-cgi-bin
sudo service apache2 restart

2- modifier le fichier "000-default.conf"

sudo nano /etc/apache2/sites-available/000-default.conf

ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
<Directory "/usr/lib/cgi-bin/">
Options ExecCGI FollowSymLinks
Require all granted
AddHandler fcgid-script .fcgi
</Directory>

sudo service apache2 restart

# tester que les configurations fonctionnent
http://localhost/cgi-bin/qgis_mapserv.fcgi?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetCapabilities

3- Installation du client Lizmap

# vérifier la version à installer en accord avec QGIS-server
# github : https://github.com/3liz/lizmap-web-client
# pour les versions : https://github.com/3liz/lizmap-web-client/wiki/Versions
# pour connaitre la version installée de qgis-server il faut lancer qgis_mapserv.fcgi :  
/usr/lib/cgi-bin/qgis_mapserv.fcgi

cd /var/www/
# choisir sa version de Lizmap
VERSION=3.5.0
# va télécharger lizmap avec la version voulu
sudo wget https://github.com/3liz/lizmap-web-client/archive/$VERSION.zip
# dézipper
sudo unzip $VERSION.zip
# créé un lien symbolique ou raccourci depuis /var/www/html/lizmap qui appelle /var/www/lizmap-web-client-$VERSION/lizmap/www/
sudo ln -s /var/www/lizmap-web-client-$VERSION/lizmap/www/ /var/www/html/lizmap
# supprimer le dossier zip maintenant unutil
sudo rm $VERSION.zip
# on va dans l'application installée lizmap-web-client
cd /var/www/lizmap-web-client-$VERSION/
# on met à jour les droits?
sudo lizmap/install/set_rights.sh www-data www-data
sudo lizmap/install/set_rights.sh
# on va dans le dossier de configuration
cd lizmap/var/config
# on copie les fichiers de copie
sudo cp lizmapConfig.ini.php.dist lizmapConfig.ini.php
sudo cp localconfig.ini.php.dist localconfig.ini.php
sudo cp profiles.ini.php.dist profiles.ini.php

Dans un nouveau termnial

# installation des modules complémentaire pour le PHP
# attention à la version de php!
sudo apt install xauth htop curl libapache2-mod-php7.3 php7.3-cgi php7.3-gd php7.3-sqlite3 php7.3-xml php7.3-curl php7.3-xmlrpc php7.3-pgsql python-simplejson
# on remet la variable VERSION avec la version de lizmap
VERSION=3.5.0
# on retourne dans lizmap-web-client
cd /var/www/lizmap-web-client-$VERSION/
# error! avec sudo php lizmap/install/installer.php
# resolution : https://github.com/3liz/lizmap-web-client/issues/1603
sudo apt install composer
cd /var/www/lizmap-web-client-$VERSION/lizmap
sudo composer install --ignore-platform-reqs
sudo php install/installer.php
# dans dosier config
cd /var/config
sudo nano localconfig.ini.php
# ajouter à la fin
[modules]
lizmap.installparam=demo
ctrl+O pour enregistrer
# on se remet dans le dossier lizmap client 
cd /var/www/lizmap-web-client-$VERSION/
# on change le propriétaire des dossier temp, var, www et qgis pour :www-data
sudo chown :www-data temp/ lizmap/var/ lizmap/www lizmap/install/qgis/ -R
# on donne au propriétaire les tous les droits (et les groupes associés), les autres utilisateurs n'ont pas les droits d'écriture
sudo chmod 775 temp/ lizmap/var/ lizmap/www lizmap/install/qgis/ -R


# Vérifier le serveur lizmap
http://localhost/lizmap


# démarrer un projet démo avec des cartes de test
sudo lizmap/install/reset.sh install --keep-config --demo

# copier un dossier avec le projet à mettre dans lizmap
sudo cp -R /home/louismaniere/Documents/Projets/lizmap/projet_qgis/kaoa_plugin_qgis /var/www/lizmap-web-client-3.5.0/lizmap/install/qgis









