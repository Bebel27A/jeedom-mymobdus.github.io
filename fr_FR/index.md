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

![WAGO](../images/WAGO_adr.jpg)


Dans ce document, vous voyez d'autres informations, comme des Byte ou Double word, mais ça ne sera pas utilisé pour le ModBus. Nous utilisons donc les I, Q et M, ainsi que les X et W.

Exemple, pour la première entrée, on peut avoir soit %IW0 (16 bits) soit %IX0.0, %IX0.1, ... , %IX0.15 (soit les 16 bits du mot, mais adressable un par un)


Parlons modbus, nous avons dans le module 2 "data type":

![WAGO](../images/WAGO_types_reg.jpg)

Pour le moment, je n'ai pas trouvé la différence entre Input Register et Holding Register, ni entre Coils et Discrete Imputs, et j'ai réussi à tout faire avec Coils et Holding Register, donc je ne parlerais que de ces 2 types.

Comment trouver les adresses ModBus correspondant aux %I, %Q, %M ? 

![WAGO](../images/WAGO_exemple.jpg)

Donc pour simplifier : 
- %IX0.0 -> %IX31.15 ont les adresses 0 à 511
- %MX0.0 -> %MX1279.15 ont les adresses de 12888 à 32750
Je ne parle pas des %QX car c'est un peu particulier et j'en parle après.


Maintenant ça va devenir plus compliqué, on va parler des mots et meme si les mots permettent de lire les mmêmes informations, les adresses sont différentes.
Par exemple, si je veux QX0.3, ça correspond au 4è bit sur mot de sortie 0, soit %QW0 bit 3.

J'espère que vous avez suivi, car avec le modbus, on ne peut pas lire un %QX, on doit lire un %QW et ensuite séparer chaque bit dans un virtuel comme indiqué plus haut dans cette documentation.

Et pour couronner le tout, %QW0 a l'adresse 512, %QW1 à l'adresse 513, ... 

Bon allez, pour vous simplifier la tâche, j'ai créé un document excel pour les premières adresses, vous le trouverez ici : 
https://github.com/Bebel27A/jeedom-mymobdus.github.io/blob/master/fr_FR/WAGO_adressage.xlsx

**Voilà, maintenant vous connaissez l'adressage, on va entrer dans le vif du sujet**

Nous avons donc notre Jeedom, notre Wago, ils communiquent via le plugin. Parfait !
On peux maintenant faire 3 choses : 
- récupérer l'état des entrées %IX et %IW
- récupérer l'état des sorties %QW (et via des virtuels les %QX)
- lire et écrire dans des registres mémoire (%MX ou %MW)

Ne pensez pas que vous pourrez directement écrire sur une sortie pour allumer une lampe, ça ne fonctionnera pas, il faut que ce soit l'automate qui active l'entrée.
**Donc les entrées et sorties sont en fait en lecture seules** (je peux me tromper car je n'ai pas fait trop de tests, mais de toute façon, pour éviter les soucis c'est nettement mieux de faire comme ça)

Rapidement, voici comment lire les informations via jeedom
Pour lire %IX0.0 : 

![IX](../images/WAGO_jeedom_IX.jpg)

Pour les %QW : 

![QW](../images/WAGO_jeedom_QW.jpg)

Et pour écrire les %MX (le principe est le même pour les MW)

![MX](../images/WAGO_jeedom_MX.jpg)

Voilà, avec ça vous pouvez lire les entrées & sorties, ainsi qu'écrire les MX
Quelques explications sur mes MX, ici j'ai voulu tester 3 fonctions avec la lampe de test que j'ai a côté de moi.
1. Simuler l'appuis sur l'interrupteur
1. Forcer l'extinction
1. Forcer l'allumage

Par contre, vous vous en doutez, ça ne suffit pas, ici on met juste les variables suivantes à 1 puis 0 (simuler un appuis sur interrupteur virtuel)
1. Addr 12337 -> %MX3.4  (pour simuler l'appuis sur l'interrupteur de la pièce)
1. Addr 12352 -> %MX4.0  (pour forcer l'allumage de la lampe Spots1)
1. Addr 12353 -> %MX4.1  (pour forcer l'extinction)

Il faut maintenant adapter le programme de l'automate dans CodeSys




(Travail en cours, ça prendra 1 ou 2 jours, revenez voir bientot)



FAQ
===

Si l’état ne remonte pas au niveau du virtuel ==> redémarrer le démon MyModbus

Merci à @Anthony_Ferreira pour ce début de documentation sur les automates Crouzet
