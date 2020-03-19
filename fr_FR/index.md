Présentation
===

Le Plugin MyModBus sert à communiquer en protocole Modbus via plusieurs types de Liaison.

	- Liaison modbus Ethernet
	- Liaison Série Mode RTU ( A venir )

Il est compatible avec plusieurs types d’automates (Crouzet, IPX  , Wago …)

Configuration du plugin
===

Après téléchargement du plugin, il vous suffit juste d’activer et d’installer les dépendances Mymodbus (clic sur le bouton Installer/Mettre à jour)

![Config1_Crouzet](../images/plugin_ok.png)


Création d'un équipement 
===

- Avant de démarrer le demon , il faut commencer par créer un équipement modbus :

![Config1_Crouzet](../images/ajout.png)

Configuration d'un équipement  .
===

![Config1_Crouzet](../images/creation_equipement.png)

Vous retrouvez ici toute la configuration de votre équipement :

	Nom de l’équipement Mymodbus : nom de votre équipement Mymodbus,

	Objet parent : indique l’objet parent auquel appartient l’équipement,

	Catégorie : les catégories de l’équipement (il peut appartenir à plusieurs catégories),

	Activer : permet de rendre votre équipement actif,

	Visible : rend votre équipement visible sur le dashboard,


En-dessous vous retrouvez la liste des commandes :

	Nom : le nom affiché sur le dashboard,

	Afficher : permet d’afficher la donnée sur le dashboard,

	Tester : permet de tester la commande
	


Exemple de configuration pour un automate Crouzet
===

- Ajout d’un équipement de type Crouzet_M3

![Config1_Crouzet](../images/creation_crouzet.png)

- Une fois la configuration renseigner on passe à l’ajout des commandes par exemple celle de type "info" : 

![Config1_Crouzet](../images/info_crouzet.png)

- Puis les commandes de type actions :

![Config1_Crouzet](../images/action_crouzet.png)


- Une fois cliqué sur sauvegarder le démon va démarrer automatiquement et les commandes seront opérationnelles 

Petit plus :) : 

	- Jeedom recherche toutes les jours à 00h30 s’il y a un automate à mettre à l’heure , si oui il le fait .


Création d'un virtuel
===

Pour se faire vous devez obligatoirement avoir installé le plugin “virtuel” 

![Config1_Crouzet](../images/virtuel.png)

Il faut maintenant créer les commandes du virtuel pour cela on s’appuie sur celles crées précédemment dans le plugin MyModbus:

- La commande info : 

	- #[Cuisine][Cuisine][MODBUS_ETAT_ECL_CUISINE]# &2 // Cette commande info nous permet de récupérer l’état sur le bit n°2

![Config1_Crouzet](../images/info_virtuel.png)

- Puis la commande action :

	- #[Cuisine][Cuisine][MODBUS_BP_ECL_CUISINE]# 

![Config1_Crouzet](../images/action_virtuel.png)

Configuration d'un WAGO
===

Dans cette partie, je vais parler de la configuration du plugin pour un automate WAGO 750-x

Petite explication sur l'adressage WAGO. Nous ne parlerons ici que des Entrées %I, des Sorties %Q et des mémoires %M
Chacune de ces adresses peut être lue et/ou écrite sous forme de bit (0 ou 1) ou de mot (16 bits = de 0 à 65535)

Exemple, pour la première entrée, on peut avoir soit %IW0 (16 bits) soit %IX0.0, %IX0.1, ... , %IX0.15 (soit les 16 bits du mot, mais adressable un par un)


(Travail en cours, ça prendra 1 ou 2 jours, revenez voir bientot)



FAQ
===

Si l’état ne remonte pas au niveau du virtuel ==> redémarrer le démon MyModbus

Merci à @Anthony_Ferreira pour ce début de documentation sur les automates Crouzet
