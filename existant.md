L'existant comprend 2 applications WEB : CodingPool et CodeGuard

Une interface utilisateur ,codé en HTML, CSS, Vue.js, donne accès aux tutoriels internes et externes référencés par
les utilisateurs de l'application. Un back-end , codé en python avec le framework Flask, envoie l'ensemble des
ressources liées aux tutoriels et aux prescripteurs, auteurs et préparateurs de ces contenus pédagogiques en ligne.
Enfin une base de données, sqlite, permet de rendre les données persistante d'une connexion à l'autre.


Le site est une application web monopage (ou single page application, SPA), cet-à-dire une application web accèssible 
via une page web unique. Le but est d'éviter le chargement d'une nouvelle page à chaque action demandée, et fluidifier
ainsi l'expérience utilisateur. Cette interface est comprise dans un unique fichier html qui sera rendu par le serveur
lors de la première connexion. Seul les parties dynamiques de la page, les labels et tutoriels, sont rechargées 
dynamiquement grâce à l'architecture AJAX. 

application monopage
tri de tutoriel
inscription connexion

plan
descriptions
critiques 


Voici la liste exhaustive des fonctionnalités qui requière une communication entre le CLIENT et le SERVEUR :
-obtenir un jeu de tutoriels et leur étiquettes discriminantes de plus haut niveau
-filtrer les tutoriels
-créer un compte utilisateur
-se connecter à un compte utilisateur
-éditer la hiérarchie des labels
-ajouter un tutoriel dans la base de données
-afficher les publications d'un utilisateur donné
-authentifier un compte (admin)



travail à implémenter :
-l'existant n'utilse pas assez les composants vuejs. Les composants pourraient-être décomposés en sous composants
 indépendants. Regrouper le code en sous composants indépendants augmente la lisibilité, la maintenabilité et 
 la réutilisabilité du code. Les composants existants sont des sortes de couteaux suisses et leur rôle devient
 incertain. Par exemple, le panneau des résultats affiche les résultats du filtrages des tutoriels, 
 les publications de chaque utilisateur, les formiulaires de connexion et inscription.
 Chacun de ces exemples nécessiterait un composant à part entière. L'implémentation existante n'est pas adapté
 à la conception de l'application monopage qui doit afficher diverse éléments dans une même partie de l'interface
 graphique (panneau des résultat). L'implémentation a accumulé un grand nombre de rendu conditionnelle sur un même
 composant. Par la suite d'autre fonctionnalité devaient apparaitre dans cette même partie de l'interface mais 
 le développeur à choisi d'abandonner le rendu conditionnel et à créer une nouvelle page html. Le principe 
 d'application monopage n'était plus respecté.

 -L'API permet au client de créer, mettre à jour ou récupérer des données sur le serveur. 
  Ces données concernent différents objet conceptuel de l'application codingpool : 
  les étiquettes, les tutoriels, les utilisateur.
  Les données sont renvoyés dans le format JavaScript Notation Object (JSON). Ce format est 
  directement interprétable par le viewModel qui sert à afficher des variables dans la page HTML.
  L'API évite le rafraichissement total de la page. Les quantités de données échangé entre le serveur et le 
  client diminue et ainsi les performances de vitesse de réaction de l'application augmentes.
  Cependant ces échanges de données ont tout de même un coup sur la performance. Il est donc préférable de 
  diminuer ces échanges au strict minimum. Malheuresement l'existant échange des données avec le serveur 
  constament. L'implémentation du design partern store serait bien adapté au filtrage des tutoriels qui 
  représente la plupart des échanges avec le serveur. Ce design partern consiste à récupérer toutes les
  données du serveur afin de les traités sur le client. Nous pourrions donc récupérer tout les tutoriels et
  étiquettes pour implémenter un filtrage local qui ne bloquerait pas le serveur.
  Ce design patern a des inconvénients. Le téléchargement de l'ensemble des données du serveur peut-être long
  et les données téléchargées sur le client peuvent ne plus être à jour. 

-A l'origine codingpool devait réutiliser un projet, labelstower, qui implémente le système de tri par étiquette.
 Au cours du développement labelstower a fusionné avec codingpool. Les fonctionnalités de labelstower n'était
 plus distingeable du reste de l'application. Nous devrons donc isolé les fonctionnalités du tri par étiquette et
 le distribuer sous la forme d'un module python.  
 Dans le contexte de création de module nous avons décidé d'isolé le front du back. L'interface graphique étant 
 propre à chaque projet l'intérêt de distribuer une interface avec la distribution labelstower est nulle.

 -L'existant propose déjà une charte graphique élaborer sur le de la piscine ainsi qu'une structure globale de
 l'interface graphique. Nous pourrons réutiliser la charte graphique ainsi que la structure proposée.

 -La base de données de l'application existante n'est pas une base de données relationnelle. Elle n'utilise pas 
 les contraintes de clés étrangères. Le schéma de la base de données devra intégrer la contrainte de clé étrnagère
 pour garantir la pertinence des données. Par ailleurs, la base de données contient des informations qu'il faudra 
 intégrer à la nouvelle base de données.

 -On remarque l'absence de test unitaire. Les tests unitaires garantisse la non régréssion du code. Il servent 
  également de documentation. 

Fonctionnalités :
+ interdir un label
+ obliger un label
+ filtrer les tutoriels
+ modifier la langue de navigation (en, fr) asynchrone ?
+ créer un compte utilisateur
* se connecter à son compte utilisateur
+ modifier la hierarchie des labels
+ ajouter un tutoriel
+ associer des utilisateurs aux rôles de comtribueur (prescriber), préparateur (preparator), demandeur (requestor)
+ associer un statut à l'élément ajouté 
+ associer un ou plusieurs labels à un tutoriel
+ gestion du statut non authentifié
+ gestion du statut d'admin
- envoie d'e-mail
- gestion du statut authentifié

interface utilisateur:
+ recherche graphique autour du thème de la piscine
+ fluidité de l'application
+ message d'information de l'API

Codeguards est une application WEB de démonstration de fonctionnement du module d'authentification flask_login.


Codeguards est une application WEB de démonstration. Elle implémente un certain nombre de fonctionnalités liés
au compte utilisateur :
Fonctionnalités existantes :
+ créer un compte utilsateur
+ se connecter/déconnecter d'une session utilisateur
+ envoyer un courrier électronique
+ authentifier un mail utilisateur
+ créer, supprimer, modifier un blog
+ afficher les posts
- rôles utilisateursle principe de compte utilisateur

Cette application de démonstration doit-être réutiliser pour construire un système d'authentification 
multi-utilisateurs sur deux applications WEB du laboratoire : CodingPool et PSPA.

Pour rendre l'application de démonstration réutilisable les services rendu par l'application de démonstration 
doivent pouvoir être rendu sous la forme de microservice auquel n'importe quelle application pourrait avoir 
accès via le protocole http.

Pour trasformer l'application de démonstration en micro service nous proposons de distribuer les fonctionnalités 
sous la forme d'une blueprint, codegiards. Cette blueprint pourra être enregistré dans n'importe quelle application
Flask qui souhaite proposer un système d'authentification à ses utilisateurs.

Les utilisateurs sont enregistrés sur une base de données. Lorsq'un utilisateur souhaite se connecter à son compte
utilisateur, il pourra y accèder en s'identifiant grâce à son mail et mot de passe.

Un utilisateur porte les caractristique suivante : id, username, mail, password, authenticated.

-L'application n'est pas fonctionnelle. login_manager n'est pas implémenté.

-L'aplication CodeGuards suit l'architecture CLIENT/SERVEUR. Le serveur 

 -Il existe trois statuts d'utilisateur
  enregistrés : l'utilisateur a été enregistré dans la base de données.
  authentifiés : l'utilisateur a authentifié son adresse électronique
  administrateurs : l'utilisateur fait parti de la liste des administrateurs.
  Pour rendre plus explicite les différents rôles de l'utilisateur, nous allons les formaliser dans la 
  base de données. Chaque utilisateur sera associé à un rôle qui évoluera. Des droits d'accès seront 
  attribuées à chacun de ces groupes.


-Démarrage de l'application avec un environnemeent virtuel.

-dépendance : flask, flask-mail, jinja, flask-login, chryptography, sqlalchemy

-base de données : post, user

-blueprint : auth, 

-cli (init_db)


GLOSSAIRE : 
-application monopage
-design patern store

Description de l'interface utilisateur

CodingPool est une application WEB créer par Cyril Mammar et David Chamont entre 2017-2018.
Elle est constitué d'une interface utilisateur écrite en Vue.js, un Framework javascript, et
d'un back-end en Flask, un Framework Python.
L'interface nous transporte à la piscine grâce à plusieurs élements graphiques faisant référence
à cet univers : fond de picine carlé, nageur, plongeur, noyer, bouées(Cf. images). 
L'interface a été conçu pour être simple et facile d'accès. Elle est constitué d'un bandeau
supérieur qui comprends le titre de l'application, CodingPool, et des bouées anglaise, française.
Ci-dessous le panneau de labels et de résultats contenant respectivement des étiquettes et des 
tutoriels. Enfin un bandeau inféreur situé en dessous des panneaux est constitué d'un texte 
d'information sur le projet et ces acteurs ainsi que du menu de navigation incluant les items : 
"Inscription" et "Connexion".
L'utilisateur peut interagir avec l'ensemble de ses éléments graphiques grâce à la souris. Nous 
détaillerons l'ensemble des interactions ci-après. Nous reviendrons également sur les panneaux
de labels et résultats peu détaillé jusqu'à présent.
Le bandeau supérieur offre des contrôles qui agissent sur l'ensemble de la page.
L'utilisateur peut rafraichir la page ou modifier la langue du site en cliquant respectivement
sur le titre ou les bouées américaines et française.
Les panneaux de labels et résultats sont les principaux éléments de l'interface.
Le panneaux de labels est constitué d'une liste d'étiquettes sélectionnables. Chaque étiquette
porte un nom et est sélectionnable en cliquant sur l'image du nageur ou du noyer. L'image du 
nageur permet de rendre obligatoire l'étiquette sélectionnée tandis que l'image du noyer interdit
l'étiquette sélectionnée.
Les sélections de l'utilisateur apparaissent dans une liste, la liste des étiquette sélectionnées,
au-dessus de la liste des étiquettes sélectionnables. Chaque étiquette sélectionnée porte un nom et
l'image correspondant au type de sélection. Les étiquettes sélectionnées sont déselectionnées en 
cliquant sur l'image du nageur pour les étiquettes rendu obligatoire ou en cliquant sur l'image du 
noyer pour les étiquettes interdites.
Le panneau de résultats est polymorphe. Par défaut c'est la liste des tutoriels résultant des 
opérations de filtrage effectué avec les étiquettes du panneau de labels. Regardons de plus près
la constitutions d'un tutoriel dans un premier temps puis nous nous interesserons aux différents 
résultats affichés dans le panneau de résultats par la suite.
Chaque tutoriel est constitué d'un nom, du nom de son auteur, préparateur ou demandeur et de la date 
de publication du tutoriel. Le nom du tutoriel ainsi que celui de son publicateur est cliquable. 
Le nom du tutoriel est un lien vers le tutoriel tandis que le nom du publicateur filtre les résultats 
afin de ne garder que les tutoriels du publicateur dans le panneau des résultats. Les tutoriels sont 
divisés en trois listes selon le rôle joué par le publicateur : demandeur, préparateur ou auteur.
Le bordereau inférieur offre des contrôles agissant sur le panneau de résultats. Les items du menu
de navigation inscription et connexion affichent respectivement un formulaire d'inscription et un
formulaire de connexion.

Implémentation de l'interface

Comme nous l'avons vu précédement, l'interface utilisateur est écrite en Vue.js. Vue.js est un framework
javascript basé sur le design patern Model View ViewVModel (MVVM). Ce design patern permet de lier de 
manière dynamique un modèle et une vue. Ainsi lorsque le modèle est modifié, la vue se met à jour et 
inversement (binding). 
L'existant est composé de quartre modèle : header, hierarchy, result, footer qui correspondent 
respectivement au  bordereau supérieur, panneau de labels, panneau de résultats et bordereau inférieur. 
Nous retrouvons donc les 4 élements graphiques vue ci-avant. Chacun des modèles à un comportement, 
les méthodes et des états, les données. L'utilisateur peut modifier l'état du modèle par l'intermédiaire des 
méthodes qui sont appelées lorsque l'utilisateur déclenche un événement via un élément de l'interface.
Par exemple l'image du nageur, à gauche d'une étiquette sélectionnable, déclenche la méthodes 
"add_label_to_old_tab" qui ajoute l'étiquette sélectionnée à la liste "old_labels_tab"
, liste des labels imposé au tutoriels filtrés. Cette liste est ensuite utilisée par le système pour 
mettre à jour le modèle result et ainsi afficher uniquement les tutoriels qui correspondent au nouveau
critère de sélection(cf. schéma pour clarifier tout ça).
Hors mis ces modèles de l'application monopage, il existe d'autre modèle associé à d'autre page html non
intégrées au site en production.