# Changelog MyModbus beta

## TODO
- Permettre un temps d'attente avant la première requête (compatibilité avec Huawei SUN2000)
- Templates : exporter, importer (en json) et éventuellement éditer des templates
- Commande action avec la valeur d'une commande Jeedom en tant que valeur
- Passer le niveau de log à la volée en cas de changement
- Passer les modifications de configuration à la volée lors de la sauvegarde sans redémarrer le démon
- Permettre 3 types de lectures :
  - Polling toutes les x secondes (comme actuellement)
  - Cyclique sans pause entre les cycles : tester si ça fonctionne et ne génère pas une charge CPU trop importante
  - Sur déclenchement
- Documentation :
  - Ajouter la méthode pour la mise à l'heure des automates Crouzet et Zelio
  - Documenter les nouvelles fonctionnalités

## 23/03/2023 V2.0 beta7
- Correction d'une erreur lors de la vérification des plages

## 23/03/2023 V2.0 beta6
- Liste déroulante pour le choix de la plage de registres (documentation ok)

## 21/03/2023 V2.0 beta5
- Lecture d'une plage d'adresses en une fois et assignation indirecte des commandes info :
Version avec une configuration permettant une meilleure compatibilité

## 19/03/2023 V2.0 beta4
- Lecture d'une plage d'adresses en une fois et assignation indirecte des commandes info (à documenter)

## 17/03/2023 V2.0 beta3
- Correction du bug qui supprimait toutes les commandes au moment de sauvegarder la configuration d'un équipement

## 16/03/2023 V2.0 beta2
- Correction de l'installation des dépendances
- Logging au niveau paramétré dans Jeedom, même pour le démon
- Ajout de l'ID dans les commandes
- Ecriture au moment où la commande est lancée dans Jeedom et plus à la fin du cycle (polling)
- Possibilité de rajouter un temps d'attente après l'écriture d'une valeur fixe
- Plus d'informations sont loggées en cas d'exception lors des lectures et écritures

## 10/03/2023 V2.0 beta1
- Réécriture complète du plugin afin de gérer un maximum de modes et de formats de données

## 22/01/2020 V1.3
- Résolution du bug sur le retour des valeurs, des équipements à IP commune.

## 18/01/2020 V1.2 b
- Découverte d'un bug sur la lecture d'une même ip avec un unit différent , En cours de résolution 
- correction du script d'ecriture ( ajour de l'unit id ) essais sur un automate wago ok  

## 28/12/2019 V1.1 S
- passage en stable ( demande en cours ) 

## 14/01/2020 V1.2 b

- Correction bug sur sauvegarde
- Mise à jour visuel commandes
- Mise en service du NTP pour crouzet à 00h30 si activé
