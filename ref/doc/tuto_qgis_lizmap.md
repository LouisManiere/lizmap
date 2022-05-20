# Création et diffusion d'une carte interactive avec QGIS et Lizmap

# Lizmap

Lizmap est un outil de création et de diffusion de carte interactive qui repose sur QGIS Server.
La carte est créée à l'aide du plugin QGIS Lizmap qui permet de paramétrer la carte, ses fonctionnalités et la mise en page. Le plugin crée un ensemble de fichier qui doivent être copié sur le dossier du serveur qui contient les cartes et les données à diffuser. Les données doivent donc être dans le même dossier qui contient le projet, dans un dossier data par exemple.
Les fichiers sont transférés dans le dossier du serveur en FTP à l'aide d'un logiciel comme Filezilla.

# Diffuser une carte Limap

Installer l'extension Lizmap de QGIS
Créer et mettre en forme le projet QGIS, un projet est nécessaire par carte que l'on souhaite diffuser.
**Attention, le projet doit être enregistrer en .qgs et non .qgz qui est l'extension par défaut !**

Ressource  :
Guide de l'éditeur
* https://docs.lizmap.com/current//fr/publish/index.html
* https://docs.lizmap.com/current/fr/publish/quick_start/project_for_web.html?highlight=projet%20web#prepare*a*qgis*project*for*web
* https://docplayer.fr/6742145*Workshop*foss4g*fr*lizmap*publier*vos*cartes*qgis*sur*internet.html

# Paramétrer le projet et les couches

## Paramètres du projet

Aller dans Projet/Propriétés, onglet QGIS Server.

Ici on définit les paramètres généraux de la carte, les éléments importants à remplir sont :
* **Nom court** (attention sans espace ni accent)
* **Titre** (titre qui sera affiché sur Lizmmap)
* **Organisation** (ex : Metis*Réseaux)
* **Personne** (auteur)
* **Rôle**
* **E*Mail**
* **Résumé**
* **Capacités WMS**
  * **Etendue annoncée** (se mettre sur une emprise plus grande que l'emprise des Couches)
  * **Restreindre les SCR** (mettre par défaut EPSG:3857 et ajouter par exemple pour la France EPSG:2154)
  * **Exclure les mise en page** (si on ne souhaite pas pouvoir exporter la carte avec un des composeurs QGIS du projet)
  * **Exclure les couches** (ajouter les couches que l'on ne souhaite pas voir du Lizmap)
* **Capacités WMTS** (cocher **Publié** pour permettre de générer un flux raster WMTS)
* **Capacités WFS** (cocher **Publié** pour permettre de générer un flux vecteur WFS)




* L'**Etendue annoncée**
* **Restreindre les CSR** mettre par défaut EPSG:3857 et ajouter par exemple pour la France EPSG:2154
* **Exclure les couches** si des couches ne sont pas nécessaire pour la carte à diffuser
* Des flux WMTS (données au format raster) et des flux WFS (données vecteurs) peuvent être générés à partir des couches disponibles. Pour les générer il faut cocher les couches à publiées.

La validité de la configuration peut être testée en bas de l'onglet.

## Paramètre des couches

Dans les propriétés de la couches, onglet QGIS Server.
On peut définir les métadonnées de la couche qui seront sur la carte Lizmap.

# Générer une carte lizmap

## Information
L'onglet information permet d'ajouter un serveur pour rester informer des nouvelles versions.

## Options de carte
Le principal intérêt est d'ajouter les outils de la carte, les échelles des zooms, l'emprise initiale.
Les échelles permettent de déterminer les différents niveau de zoom lors de la navigation avec une suite de nombre séparée par des virgules. Les échelles par défaut ne sont en générales pas pertinentes pour une bonne navigation. Pour une carte permettant de voir au niveau d'une rue jusqu'à l'échelle mondiale voilà un exemple  :
100, 1000, 5000, 10000, 25000, 50000, 100000, 200000, 500000, 1000000, 2000000, 5000000, 10000000, 20000000, 50000000, 100000000, 150000000

## Couches
**Titre** modifie le nom de la couche affiché dans Lizmap et **Résumé** sa description.

Par défaut les couches de la carte Lizmap ne sont pas visibles, il faut cocher la case **Cochée** de la partie légende pour les rendre visibles à l'ouverture de la carte sur Lizmap.
On peut également paramétrer les popups de chaque couche qui s'afficheront au clique de la souris.
Un fond de carte autre que ceux proposer par Lizmap peut être aussi défini avec l'option **Fond de carte** de la partie légende.

## Fonds de carte
Dans l'onglet **Fond** on peut cocher les fonds de carte que l'on souhaite pouvoir choisir pour la carte. Le fond **OSM Mapnik** correspond au fond OSM standard, **OSM Stamen Toner** correspond à un fond sobre plutôt administratif. L'ajout des fonds de carte de l'IGN ne nécessite pas de clé.
Le fond de carte par défaut se définit ensuite dans **Fond de carte actif au démarrage**.
On peut définir un fond de carte personnel dans l'onglet **Couches** en cochant **Fond de carte** dans les options de légende.

# Ajouter la carte sur lizmap
