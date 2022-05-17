# Création et diffusion d'une carte interactive avec QGIS et Lizmap

# Lizmap

Lizmap est un outil de création et de diffusion de carte interactive qui repose sur QGIS Server.
La carte est créée à l'aide du plugin QGIS Lizmap qui permet de paramétrer la carte, ses fonctionnalités et la mise en page. Le plugin crée un ensemble de fichier qui doivent être copié sur le dossier du serveur qui contient les cartes à diffuser. Les fichiers sont transférés dans le dossier du serveur en FTP à l'aide d'un logiciel comme Filezilla.

# Créer le projet

Installer l'extension Lizmap de QGIS
Créer et mettre en forme le projet QGIS, un projet est nécessaire par carte que l'on souhaite diffuser.
**Attention, le projet doit être enregistrer en .qgs et non .qgz par défaut !**

# Paramétrer le projet et les couches

Ressource  :
- https://docs.lizmap.com/current/fr/publish/quick_start/project_for_web.html?highlight=projet%20web#prepare-a-qgis-project-for-web
- https://docplayer.fr/6742145-Workshop-foss4g-fr-lizmap-publier-vos-cartes-qgis-sur-internet.html

## Paramètre du projet

Aller dans Projet/Propriétés, onglet QGIS Server.

Ici on définit les paramètres généraux de la carte, les éléments importants à remplir sont :
- Le **Nom court**
- Le **Titre**
- L'**Etendue annoncée**
- **Restreindre les CSR** mettre par défaut EPSG:3857 et ajouter par exemple pour la France EPSG:2154
- **Exclure les couches** si des couches ne sont pas nécessaire pour la carte à diffuser
- Des flux WMTS (données au format raster) et des flux WFS (données vecteurs) peuvent être générés à partir des couches disponibles. Pour les générer il faut cocher les couches à publiées.

La validité de la configuration peut être testée en bas de l'onglet.

## Paramètre des couches

Dans les propriétés de la couches, onglet QGIS Server.
On peut définir les métadonnées de la couche qui seront sur la carte Lizmap.

# Générer la carte lizmap

## Information
L'onglet information permet d'ajouter un serveur pour rester informer des nouvelles versions.

## Options de carte
Le principal intérêt est d'ajouter les outils de la carte, les échelles des zooms, l'emprise initiale.

## Couches
On peut modifier les métadonnées paramétrées dans les propriétés de la couche.
Par défaut les couches de la carte Lizmap ne sont pas visibles, il faut cocher la case **Cochée** de la partie légende pour les rendre visibles à l'ouverture de la carte sur Lizmap.
On peut également paramétrer les popups de chaque couche qui s'afficheront au clique de la souris.
Un fond de carte peut être aussi défini avec l'option **Fond de carte** de la partie légende.

## Fonds
On peut ajouter un des fonds de carte paramétrés depuis Lizmap.

# Ajouter la carte sur lizmap
