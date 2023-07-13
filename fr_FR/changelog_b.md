# Changelog MyModbus beta

## TODO
- Templates : exporter, importer (en json) et éventuellement éditer des templates
- Documentation :
  - Ajouter la méthode pour la mise à l'heure des automates Crouzet et Zelio
  - Documenter les nouvelles fonctionnalités (à partir de la beta12)

## 14/07/2023 V2.0 beta22
- Le bouton d'ajout de commande en bas du tableau des commandes fonctionne dorénavant comme attendu
- Les retours NaN sont correctement gérés

## 06/06/2023 V2.0 beta21
- Forçage de la version pymodbus 3.2.2 pour éviter des erreurs avant de trouver une meilleure solution

## 10/05/2023 V2.0 beta20
- Correction des logs des écritures en mode bi-maître
- Ajout de la commande info liée aux commandes action
- Ajout du bouton de création de commande en fin de tableau

## 06/05/2023 V2.0 beta19
- Deuxième tentative du mode bi-maître spécifique aux chaudières De Dietrich Diematic (merci à loustic03 de m'avoir laissé autant de temps pour tester chez lui)

## 05/05/2023 V2.0 beta18
- Prise en charge des commandes action avec une liste
- Première tentative du mode bi-maître spécifique aux chaudières De Dietrich Diematic
- Affichage de la configuration de l'endianess pour les commandes actions (merci à thomaspascal)
- Indentation du code de tout le plugin avec 2 espaces au lieu de 4

## 13/04/2023 V2.0 beta17
- Pour les commandes binaires depuis une plage de registres, les plages numériques en source sont possibles mais un filtre doit être spécifié (merci à Noyax37)

## 10/04/2023 V2.0 beta16
- Petite correction sur le log lors de l’exécution d’une commande action

## 09/04/2023 V2.0 beta15
- Amélioration de la saisie des commandes an désélectionnant les options invisibles (merci à Noyax37)
- Remontée de la valeur lue vers Jeedom par le démon si la commande est configurée avec "Répéter les valeurs identiques" à "Oui" (merci Bison pour l'astuce)
- Meilleure gestion des exceptions
- Ajout du nom de l'équipement dans les logs du démon (là où c'est possible)

## 07/04/2023 V2.0 beta14
- Les reconnexions automatiques de pymodbus sont désactivées. Les (re)connexions sont gérées par le démon (merci à thomaspascal)
- En cas de sauvegarde de la configuration, le démon se déconnecte avant de prendre la nouvelle configuration en compte (merci à thomaspascal)
- Maintien de l'ordre des commandes lors de la sauvegarde qui rajoute les commandes spéciales (merci à thomaspascal)
- Correction de l'erreur lors de la duplication d'un équipement (merci à Noyax37)
- Suppression des paramètres de configuration utilisés dans l'ancienne version (et donc le retour en version stable est rendu impossible sans restaurer un backup ou resaisir les configurations)

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
- Seuls les équipements utilisant le protocole de connexion "serial" ne peuvent pas utiliser la même interface.  
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
