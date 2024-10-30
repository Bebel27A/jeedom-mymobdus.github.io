# Changelog MyModbus beta

## TODO
- Traduction
- Ne plus utiliser le dépôt github de Bebel27 pour la documentation
- Documentation :
  - Documenter les nouvelles fonctionnalités (documentation à jour avec la version V2.0 beta55)

## xx/1x/2024 V2.0 beta56 (en cours de développement)
- Possibilité de déplacer des commandes d'un équipement à un autre afin de garder les commandes lors d'un split d'équipement en
cas d'utilisation de la même interface

## 30/10/2024 V2.0 beta56
- Correction sur les fonctions d'écriture

## 25/10/2024 V2.0 beta55

> :warning: ***Important***  
> Une réinstallation des dépendances doit être faite sans quoi le démon MyModbus ne fonctionnera pas.  
> Elle est lancée automatiquement après la mise à jour du plugin.

- Utilisation de pymodbus V3.7.4

## 24/10/2024 V2.0 beta54
- Forçage de la version de pymodbus à 3.7.3

## 16/10/2024 V2.0 beta53
- Mise à jour de jeedomdaemon (il faut relancer l'installation des dépendances)

## 07/10/2024 V2.0 beta52
- Nouveauté : inversion des doubles-mots possible
- Nouveauté : affichage de la configuration d'inversion en fonction du type de donnée

## 05/10/2024 V2.0 beta51
- Nouveauté : utilisation de la même interface pour plusieurs équipements
- Nouveauté : ajout d'une commande info 'Polling' qui contient le temps de polling recalculé actuel (si la commande n'existe pas,
sauvegardez l'équipement)
- Correction : la commande "Cycle OK" est mise à 0 dès qu'une erreur se produit et est mise à 1 dès qu'un cycle complet (lecture
de toutes les commandes info) s'est déroulé sans erreur
- Correction du mode "Sur événement" qui pouvait ne pas réagir à la commande "Rafraîchir"
- Correction du mode "Sur événement" qui rajoutait une boucle de lecture à chaque rafraîchissement
- En mode "Sur événement", suppression des tâches run_loop "done"
- Amélioration de la gestion de la connexion
- Amélioration de la gestion d'une nouvelle configuration
- Structure du démon : la classe MyModbusConfig est écrite dans un fichier dédié
- [ESSAI] Suppression effective de l'ancien répertoire 'ressources' (avec 2 S) qui n'est plus utilisé

## 26/09/2024 V2.0 beta50
- Si les valeurs saisies dans la configuration commencent ou se terminent par des espaces, ceux-ci sont ignorés
- Le polling n'est plus recalculé en cas d'erreur durant le cycle

## 25/09/2024 V2.0 beta49
- Correction de l'erreur de syntaxe qui bloquait les écritures (merci wocha-fr)

## 24/09/2024 V2.0 beta48
- Correction de la fonction eqLogic.getDeamonLaunchable (merci wocha-fr)
- Correction du type d'un index de dictionnaire (merci wocha-fr)
- Corrections de syntaxe (merci thomaspascal, Droopy et lperenna)
- [ESSAI] Gestion correcte d'un temps d'attente après erreur plus long (quelques minutes)

## 23/09/2024 V2.0 beta47

> :warning: ***Important***  
> A partir de cette version, l'inversion des mots ne sera plus nécessaire si l’architecture du CPU est identique entre
l’appareil et votre machine Jeedom. La logique a été inversée dans le module pymodbus, alors j'ai fait des fonctions à ma sauce.
Cela affecte les commandes info et action sur des variables d'au moins 32 bits.
> Veillez à bien vérifier votre configuration avant et à faire les adaptations nécessaires.

- Gestion interne du boutisme (endianess) et non plus via pymodbus
- Suppression du double log en cas d'erreur de lecture

## 22/09/2024 V2.0 beta46
- Vérification que la commande existe bien lorsqu'un changement de valeur est reçu pour éviter une erreur (merci thomaspascal)
- Affichage du bouton "Supprimer" dans le viewer de template (merci thomaspascal)
- Corrections pour les connexions série (merci wocha-fr)

## 20/09/2024 V2.0 beta45
- Correction du problème avec les templates
- Correction du problème avec l'ordre des mots d'une valeurs sur plus de 32 bits dans une plage de registres lorsque l'offset
dans la plage de registres est impaire
- Correction de la prise en charge du paramètre "port" pour les liaisons série

## 19/09/2024 V2.0 beta44
- Prise en compte de la configuration d'inversion des octets et des mots pour les valeurs lues depuis une plage de registres
(merci thomaspascal)

## 18/09/2024 V2.0 beta43
- Optimisation du verrou qui permet les requêtes afin que les écritures puissent être faites plus rapidement
- Vérification de l'état de la connexion avant chaque requête
- Le polling peut être configuré à 0.01s minimum
- Reprise de l'ancienne configuration du format de données pour les commandes action également
- Le démon n'est pas "launchable" si le venv n'est pas présent
- Suppression de l'ancien répertoire mal orthographié "ressources" (avec 2 S)

## 17/09/2024 V2.0 beta42

> :warning: ***Important***  
> 1. Avant de faire cette mise à jour, désactivez les équipements MyModbus. Faites une capture de la configuration des équipements
et des commandes. Après la mise à jour, **sauvegardez les équipements sans les activer**. Vérifiez bien la configuration des
commandes.
> 2. Si des commandes dont l'adresse d'esclave vaut 0 ne fonctionnent plus après la mise à jour, il faut passer cette valeur à 1.
Il s'agit de la valeur par défaut depuis pymodbus v3.7.0. Si les erreurs persistent, recherchez quelle est la valeur à renseigner
dans la documentation constructeur.

- Réécriture complète du démon :
  - Utilisation de bibliothèques de dev tiers pour Jeedom (jeedomdaemon, dependance.lib, pyenv.lib) (merci Mips, nebz et TiTiDom)
  - Utilisation de pymodbus V3.7.2 (à ce jour)
  - Abandon de la dépendance avec pyenv4Jeedom
  - Abandon de BinaryPayloadBuilder et BinaryPayloadDecoder appelés à disparaître du module pymodbus (dès 3.8.0 pas encore sortie)
  - Ajout des paramètres d'équipement :
    - Timeout pour la connexion
    - Nombre de tentatives en cas d'erreur de lecture
    - Temps d'attente après une erreur de lecture pour éviter d'enchainer les erreurs pour la même raison
  - Structure des appels des sous-classes pymodbus.ModbusRequest inspirée de l'intégration Modbus de Home-Assistant
  - Ajout de la commande info `Cycle OK` qui est mise à 1 si le dernier cycle de lecture s'est déroulé sans erreur, sinon 0. Cette
  commande peut être surveillée. Si elle passe à 0, c'est qu'il y a eu un problème durant le dernier cycle de lecture
  - Il n'est plus possible de modifier le niveau de log à la volée, il faut redémarrer le démon
- Page de configuration de l'équipement :
  - Plus rapide : sans appels ajax à des pages php locales
  - Le bouton 'Ajouter une commande' est flottant (merci noodom), le bouton en bas de page est supprimé
- Suppression du format bit inversé qui ne fonctionnait pas et qui est facile à mettre en place (`1 - #value#`)
- Suppression des formats int8, seuls les formats uint8 sont gardés
- Suppression du format float16
- Prise en compte de l'inversion des octets et des mots pour les chaînes de caractères

## 17/06/2024 V2.0 beta41
- Correction d'une erreur de syntaxe (merci m.georgein)
- Lors de l'exécution d'une commande action, il faut vérifier si l'équipement est actif avant d'envoyer la commande au démon

## 03/05/2024 V2.0 beta40
- Correction de syntaxe sur des messages de log du démon (merci à Jean-Baptiste)

## 15/04/2024 V2.0 beta39
- Correction de l'utilisation de la fonction `strtolower` (merci à Jean-Baptiste)

## 14/03/2024 V2.0 beta38
- Logs un peu plus détaillés en mode debug

## 11/03/2024 V2.0 beta37
- Amélioration de l'interaction avec pyenv

## 08/03/2024 V2.0 beta36
- Amélioration de l'interaction avec pyenv

## 06/03/2024 V2.0 beta35
- Initialisation de pyenv

## 04/03/2024 V2.0 beta34
- Externalisation de pyenv dans un plugin dédié
- Suppression du bouton dans la configuration du plugin pour supprimer le répertoire ressources/_pyenv

## 21/02/2024 V2.0 beta33
- Ajout d'un bouton dans la configuration du plugin pour supprimer le répertoire ressources/_pyenv
- Affichage de toute la config dans le visualisateur de template
- Possibilité d'utiliser #value# dans le champs valeur d'une commande action pour faire référence à la valeur de la commande info liée

## 17/02/2024 V2.0 beta32
- Correction pour que '0' puisse être écrit (merci à Doud)

## 16/02/2024 V2.0 beta31
- Suppression du mode bi-maître qui ne fonctionne pas
- Lors de la sauvegarde, si rien n'est précisé dans le champ valeur, définir avec `#slider#`, `#select#` ou `#color#` en fonction du cas, sinon invalider la config
- Lors de la sauvegarde si `#slider#`, `#select#` ou `#color#`, en fonction du cas, n'est pas dans le champ valeur, avertir avec une erreur.
- Invalider l'exécution d'une commande action si la valeur à écrire est vide

## 14/02/2024 V2.0 beta30 (mise à jour de la St Valentin)
- Le champ valeur est sauvegardé correctement

## 12/02/2024 V2.0 beta29
- Ajout de la gestion de templates (documentation à mettre à jour)  
Cette fonctionnalité est basée sur ce qui existe dans jMQTT
- Révision du bandeau de menu de la configuration du plugin (page d'ajout des équipements)
- Corrections de syntaxe

## 09/01/2024 V2.0 beta28
- Correction du script post-install.sh pour mettre à jour pyenv même après la restauration d'un backup de Jeedom (merci à m.georgein)

## 03/12/2023 V2.0 beta27
- Correction du script post-install.sh pour mettre à jour pyenv correctement avant d'installer python V3.11.6

## 28/11/2023 V2.0 beta26
- Correction du script post-install.sh pour mettre à jour pyenv avant d'installer python V3.11.6 (merci ngm47)

## 26/11/2023 V2.0 beta25
- Liste des paquets à installer réduite au minimum
- Passage à python V3.11.6 sous pyenv. L'étape de réinstallation des dépendances va durer plusieurs dizaines de minutes.
- Retour arrière sur une modification de la version V2.0 beta24 : le fait que le démon soit "launchable" si plusieurs équipements utilisent le même port série
- Mise à jour de la documentation
- Ajout de la possibilité de personnaliser les interfaces série (idée de jmcaous trouvée sur le Community)

## 08/11/2023 V2.0 beta24
- Correction erreur 500 à la sauvegarde d'un nouvel équipement (merci ksin)
- Le démon est "launchable" si plusieurs équipements utilisent le même port série. Dans ce cas, c'est à l'utilisateur de configurer le plugin correctement (merci indirectement à ksin)
- Petites corrections

## 02/08/2023 V2.0 beta23
- Les listes sont gérées pour les binaires également
- Les couleurs sont prises en compte

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
