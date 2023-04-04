# Changelog MyModbus beta

## TODO
- Améliorer la saisie des commandes an désélectionnant les options invisibles (merci à Noyax37)
- Templates : exporter, importer (en json) et éventuellement éditer des templates
- Documentation :
  - Ajouter la méthode pour la mise à l'heure des automates Crouzet et Zelio
  - Documenter les nouvelles fonctionnalités (à partir de beta12)

## 05/04/2023 V2.0 beta13
- Contournement de l'erreur d'affichage des paramètres d'équipement (Solution en cours)
- Correction de l'erreur lors de la duplication d'un équipement (merci à Noyax37)
- Démon : si la lecture retourne 'nan', la valeur n'est pas remontée vers Jeedom et une erreur est générée (merci à ced2001)

## 04/04/2023 V2.0 beta12
- Ajout du mode cyclique
- Ajout du mode lecture sur événement
- Le temps de polling minimum est maintenant de 1 seconde
- Mise en place des paramètres d'équipement par défaut
- Migration de la configuration de l'équipement en cas de migration depuis l'ancienne version de MyModbus
- Remontée de la valeur lue vers Jeedom par le démon uniquement en cas de changement de valeur
- Diverses optimisations

## 29/03/2023 V2.0 beta11
- Correction de l'affichage du paramètre "adresse esclave" des commandes action (merci à Noyax37 et à pilou226)

## 28/03/2023 (0:08) V2.0 beta10
- Correction de l'erreur lors de l'écriture d'un binaire (merci à ngm47)
- La pause suite à une commande action est cumulable avec l'écriture de la valeur d'une expression

## 27/03/2023 (8:57) V2.0 beta9
- Passer le niveau de log à la volée en cas de changement sans redémarrer le démon
- Passer les modifications de configuration à la volée lors de la sauvegarde sans redémarrer le démon
- Meilleure gestion de la communication entre le démon et les process PyModbusClient
- Meilleure gestion des arrêts des process
- La valeur des commandes action peut être configurée comme dans le plugin Virtuel
- Seuls les équipement utilisant le protocole de connexion "serial" ne peuvent utiliser la même interface.  
Les équipements en TCP ou UDP **peuvent** communiquer avec la même adresse IP, ça ne veut pas dire qu'ils le doivent.

## 24/03/2023 V2.0 beta8
- Correction de la fonction de validation des adresses d'une plage de registres
- Optimisation du temps de traitement des valeurs remontées par le démon
- Gestion de la reconnexion en cas de déconnexion
- Heartbeat entre le démon et Jeedom : un signal envoyé par le démon à Jeedom, si pas de réponse le démon se termine (pour éviter les zombis)
- Permettre un temps d'attente avant la première requête (compatibilité avec Huawei SUN2000)
- Validation de la configuration de sorte que deux équipements ne puissent pas utiliser la même connexion

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
